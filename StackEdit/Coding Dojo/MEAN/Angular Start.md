### Set up Express backend

```console
mkdir {{{project folder}}}
cd {{{project folder}}}
npm init -y
npm install express body-parser mongoose
touch server.js routes.js models.js controller.js
```
##### server.js
```javascript
const express = require('express')
const bp = require("body-parser")

var app = express()

app.use(bp.json())
app.use(bp.urlencoded({extended:true}))
app.use(express.static( __dirname +  '/public/dist/public' ));

require('./routes')(app)

app.listen(8000, (err)=>{
    if (err){
        console.log(err)
    } else {
        console.log("listening on port 8000...")
    }
})
```
##### routes.js
```javascript
const controller = require("./controller")

module.exports = function(app){
    app.get('/api/authors', controller.authors)
    app.get('/api/authors/:id', controller.author)
    app.post('/api/authors', controller.create)
    app.put('/api/authors/:id', controller.update)
    app.delete('/api/authors/:id', controller.delete)
    app.all("*", controller.all) // Typing into the nav bar and hitting enter or making the browser refresh will trigger the Express routes first and Angular routes second.
}
// this route will be triggered if any of the routes above did not match
app.all("*", (req,res,next) => {
  res.sendFile(path.resolve("./public/dist/public/index.html"))
});
```
##### controller.js
```javascript
const Task = require("./models")

module.exports = {
    tasks : (req, res) => {
        Task.find({}, function(err, tasks) {
            if (err) {
                console.log(err)
            } else {
                res.json({'tasks': tasks})
            }
        })
    },

    show : (req, res) => {
        Task.findOne({_id : req.params.id}, function(err, task){
            if (err) {
                console.log(err)
            } else {
                res.json({'task':task})
            }
        })
    },
    create : (req, res) => {
        console.log(req.body)
        Task.create(req.body, function(err, task){
            if (err) {
                console.log(err)
            } else {
                res.json({message: "created", "task" : task})
            }
        })
    },
    update : (req, res) => {
        Task.findByIdAndUpdate({_id : req.params.id}, req.body, {new: true}, function(err, task){
            if (err) {
                console.log(err)
            } else {
                res.json({message: "updated", "task" : task})
            }
        })
    },
    delete : (req, res) => {
        Task.findByIdAndDelete({_id : req.params.id}, req.body, function(err, task){
            if (err) {
                console.log(err)
            } else {
                res.json({message: "deleted", "task" : task})
            }
        })
    },
    all : (req,res,next) => {
	  res.send("Sorry, this page doesn't exist"))
    }
```
##### models.js
```javascript
const mongoose = require('mongoose')

mongoose.connect('mongodb://localhost/restful_task_db', {useNewUrlParser : true})

mongoose.set('useFindAndModify', false);
mongoose.set('useCreateIndex', true) //https://github.com/Automattic/mongoose/issues/6890

var TaskSchema =  new mongoose.Schema({
    title : {type: String, required : true},
    description : {type : String, default : ""},
    completed : {type : Boolean, default : false}
}, {timestamps : {createdAt : "created_at", updatedAt : "updated_at"}}
)
  
module.exports = mongoose.model('Task', TaskSchema)
```




##### Install Angular

```console
npm install -g @angular/cli
```

##### New Project
```
ng new [[public]]
cd public
ng build --watch
```



##### Build a service

```
ng g s [[service name]] (tasks)
```

##### app.component.ts
```typescript
import { Component } from '@angular/core';
import { TasksService } from './tasks.service'

@Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.css']
})
export class AppComponent {
    title = 'tasks';
    tasks : Array<object>
    one_task : object
    constructor(private _tasksService: TasksService){}

    ngOnInit(){
        
        this.title = "Restful Tasks"
    }

    return_tasks(){
        this.get_tasks_from_service()
    }

    get_tasks_from_service(){
        let observable = this._tasksService.get_tasks()
        observable.subscribe(data => {
            console.log("Tasks: ", data)
            this.tasks = data['tasks']
        })
    }

    do_this(id){
        let observable = this._tasksService.get_one_task(id)
        observable.subscribe(data => {
            this.one_task = data['task']
        })
    }

    select_change_handler(event: any){
        let observable = this._tasksService.get_one_task(event.target.value)
        observable.subscribe(data => {
            this.one_task = data['task']
        })
    }
}
```
##### app.module.ts
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { TasksService } from './tasks.service'
import { HttpClientModule } from '@angular/common/http'
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [TasksService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
##### task.service.ts
```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http'

@Injectable({
    providedIn: 'root'
})
export class TasksService {

    constructor(private _http: HttpClient) {}

    get_tasks() {
        return this._http.get('/tasks')
    }

    get_one_task(id){
        return this._http.get('/tasks/' + id)
    }
}
```
##### app.component.html
```html

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjM3NjE5NzM5LC04NDM3NjQ2ODEsMTM2NT
Q2OTQyMSwtMjA2MDQ0MjYyNiwtODY4MTUxNTM5LC0xNjAyNDc4
NDU3LDEzNDYwNDk5NywxNzAzNjk4MDcyLDI3NTM0ODQxNywtMT
AxODkyMzMyMSw1ODgwODcxMiwtMTU1MTc4MTgwNCwxMTMxMDgx
MTY0LDQ3MDkzOTkyMSwtNjg1ODg2NjMyXX0=
-->