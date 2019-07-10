```console
mkdir {{project_name}}
cd {{project_name}}
mkdir static static/images static/css views
npm init
npm install express ejs express-session body-parser
code .
```
##### create server.js
```javascript
var express = require("express");
var app = express();
app.set('views', __dirname + '/views/');
app.set('view engine', 'ejs');
app.use(express.static(__dirname + "/static"));
require('./routes')(app)
app.listen(8000, (err)=>{
  if (err) {
    console.log(err);
  } else {
    console.log("listening on port 8000")
  }
})
```
##### create controller.js
```j
##### create routes.js


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU1OTg2MzU2NywxNTc2NDg0NjQ4LDczMD
k5ODExNl19
-->