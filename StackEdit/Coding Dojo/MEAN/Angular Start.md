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
ng g s [[service name]]
```

##### app.component.ts
```typescript
import { Component } from '@angular/core';
import { HttpService } from './http.service' //add

@Component({
selector: 'app-root',
templateUrl: './app.component.html',
styleUrls: ['./app.component.css']
})

export class AppComponent {
title = 'restful_tasks';
constructor(private _httpService: HttpService) {} //add
}
```javascript
import { HttpService } from './http.service';
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY4NTg4NjYzMl19
-->