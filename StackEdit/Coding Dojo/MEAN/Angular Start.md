### Set up Express backend

```console
mkdir {{{project folder}}}
cd {{{project folder}}}
npm init -y
touch server.py routes.py models.py controller.py
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

}

}
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
ng g s [[service name]] (pokemon)
```

##### app.component.ts
```typescript
import { Component } from '@angular/core';
import { PokemonService } from './pokemon.service' //add

@Component({
selector: 'app-root',
templateUrl: './app.component.html',
styleUrls: ['./app.component.css']
})

export class AppComponent {
title = 'restful_tasks';
constructor(private _pokemonService: PokemonService) {} //add
}
```
##### app.module.ts
```typescript
import { BrowserModule } from  '@angular/platform-browser';
import { NgModule } from  '@angular/core';
import { PokemonService } from  './pokemon.service'
import { HttpClientModule } from  '@angular/common/http'
import { AppComponent } from  './app.component';

@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        BrowserModule,
        HttpClientModule
    ],
    providers: [PokemonService],
    bootstrap: [AppComponent]
})
export  class AppModule { }
```
##### pokemon.service.ts
```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http'

@Injectable({
providedIn: 'root'
})
export class HttpService {

    constructor(private _http: HttpClient) {
        this.getTasks()
        this.getATask('5d292b1435b36446c1a6d79c')
    }
    getTasks(){
        let tempObservable = this._http.get('/tasks')
        tempObservable.subscribe(data => console.log("Got our tasks!", data))
    }
    getATask(id){
        let taskObserver = this._http.get('/tasks/' + id)
        taskObserver.subscribe(data => console.log("Got task back: ", data))
    }
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MjgwMzgxNzAsMTEzMTA4MTE2NCw0Nz
A5Mzk5MjEsLTY4NTg4NjYzMl19
-->