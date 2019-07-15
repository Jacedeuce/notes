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
```javascript
import { HttpService } from './http.service';
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwOTAyODM5NCwtNjg1ODg2NjMyXX0=
-->