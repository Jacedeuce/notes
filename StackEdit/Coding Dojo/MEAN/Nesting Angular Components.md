## Nesting Angular Components

### Build new component
```console
ng generate component {{{component_name}}} - task
```
app tree:
├── app.component.css
├── app.component.html
├── app.component.spec.ts
├── app.component.ts
├── app.module.ts
├── task
│   ├── task.component.css
│   ├── task.component.html
│   ├── task.component.spec.ts
│   └── task.component.ts
├── tasks.service.spec.ts
└── tasks.service.ts

##### app.component.html
* add the selector for the nested component in the root component html
```html
...
<app-task></app-task>
...
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk5NzI0ODM2OV19
-->