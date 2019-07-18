### Set up Express backend

```console
mkdir {{{project folder}}}
cd {{{project folder}}}
npm init -y
npm install express body-parser mongoose
touch server.js routes.js models.js controller.js
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
        Task.findByIdAndUpdate({_id : req.params.id}, req.body, function(err, task){
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
	  res.sendFile(path.resolve("./public/dist/public/index.html"))
    }
```
##### models.js
```javascript
const mongoose = require('mongoose')

mongoose.connect('mongodb://localhost/restful_task_db')

var TaskSchema =  new mongoose.Schema({
    title : {type: String, required : true},
    description : {type : String, default : ""},
    completed : {type : Boolean, default : false}
}, {timestamps : {createdAt : "created_at", updatedAt : "updated_at"}}
)
  
module.exports = mongoose.model('Task', TaskSchema)
```
##### routes.js
```javascript
const controller = require("./controller")
module.exports =  function(app){
    app.get('/tasks', controller.tasks)
    app.get('/tasks/:id', controller.show)
    app.post('/tasks', controller.create)
    app.put('/tasks/:id', controller.update)
    app.delete('/tasks/:id', controller.delete)
    app.all("*", controller.all)
}
// this route will be triggered if any of the routes above did not match
app.all("*", (req,res,next) => {
  res.sendFile(path.resolve("./public/dist/public/index.html"))
});
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
eyJoaXN0b3J5IjpbNjc0ODI4MzI4LDE3MDM2OTgwNzIsMjc1Mz
Q4NDE3LC0xMDE4OTIzMzIxLDU4ODA4NzEyLC0xNTUxNzgxODA0
LDExMzEwODExNjQsNDcwOTM5OTIxLC02ODU4ODY2MzJdfQ==
-->