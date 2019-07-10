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
```javascript
module.exports = {
  index : (req, res)=>{
    var context = {pages : ['cars', 'cats']}
    res.render('index', context)
  },
  cars : (req, res)=>{
    res.render('cars')
  },
  newcar : (req, res)=>{
    res.render('newcar')
  },
  cats : (req, res)=>{
    res.render('cats', {cats : cat_arr})
  },
  cat_show : (req, res)=>{
    res.render('cat_show', {cat : cat_arr[req.params.catID-1]})
  }
}
```
##### create routes.js
```javascript
const controller = require("./controller");

module.exports = function(app){

app.get('/', controller.index)

app.get('/cars', controller.cars)

app.get('/cars/new', controller.newcar)

app.get('/cats', controller.cats)

app.get('/cats/:catID', controller.cat_show)

}
```


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTQ5OTMwMzc4LDE1NzY0ODQ2NDgsNzMwOT
k4MTE2XX0=
-->