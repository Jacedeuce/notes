##  New Node Project
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
var express = require("express")
var bp = require("body-parser")
var path = require("path")
var app = express()

app.use(bp.urlencoded({extended: true}))
app.use(express.static(path.join(__dirname, './static')))
app.use(session({
    secret: 'quotes',
    resave: false,
    saveUninitialized: true,
    cookie: { maxAge: 60000 }
}))

app.set('views', path.join(__dirname, '.views'))
app.set('view engine', 'ejs')
  
require('./routes')(app)

app.listen(8000, function(errs) {
    if (errs){
        console.log(errs)
    } else {
        console.log("listening on port 8000...")
    }
})
```
##### create controller.js
```javascript
const User = require("./models")

module.exports = {
index : (req, res)=>{
res.render('index')
},
users : (req, res)=>{
console.log("POSTDATA", req.body)

var user =  new User({name: req.body.name, age: req.body.age});
// Try to save that new user to the database (this is the method that actually inserts into the db) and run a callback function with an error (if any) from the operation.
user.save(function(err) {
// if there is an error console.log that something went wrong!
    if(err) {
	console.log('something went wrong');
    } else { // else console.log that we did well and then redirect to the root route
        console.log('successfully added a user!');
    }
    res.redirect('/')
})
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
#### Mongo
```console
sudo systemctl enable mongod.service
sudo systemctl start mongod.service
```
#### project tree
.
├── controller.js
├── models.js
├── routes.js
├── server.js
├── static
│   └── css
│       └── style.css
└── views
    └── index.ejs
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODE3Mzc4MTksNjA2NTMzMjkyLC0xOT
I4NDc3MDE2LC01NTUyOTI4MDIsMTQxMDY5NjU3NCwtNDM2NzAz
NTU2LDEzNDIxNzAxMzUsMTU3NjQ4NDY0OCw3MzA5OTgxMTZdfQ
==
-->