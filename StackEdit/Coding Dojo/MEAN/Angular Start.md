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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNjYzOTc0ODUsLTY4NTg4NjYzMl19
-->