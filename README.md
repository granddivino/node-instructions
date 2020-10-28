---Starting a Node App---
1. After you open your terminal, go to the location of where you plan to create your app
2. Make a directory (mkdir) with the name of your project.
3. Initialize npm inside the directory you made (npm init) (or npm init -y to skip the inital setup)
4. Make your entry point (touch index.js)

---Node Packages and modules---
Node modules are including using the requires(<module>) statement. These can be files on your computer, default modules like HTTPServer or fs (filesystem) or 3rd party modules. 

Install packages with npm i packagename like this:
1. Install express into your app (npm i express) 
2. Install ejs (npm i ejs)
3. Install express ejs layouts (npm i express-ejs-layouts)
4. Install axios (npm i axios)
5. Install dotenv (npm i dotenv)



---Adding Express to a Node App---
1. // Import the express module

const express = require('express')

2. // Create an instance of an express app

const app = express()

3. //Create a port to listen in on 
app.listen(8000, () => {
    console.log('Port 8000 is OPEN')
})

4. If you have Nodemon installed run it in your terminal with (nodemon)

5. If nodemon is still running from last time it was used (killall mode or CTRL + C) in your terminal


---Express Routes---
1. // Create a home route

app.get('/',(req,res)=>{
    res.send('Whatever you want here.')
})

2. // Or if you have it in a controller it would be
router.get('/',(req,res)=>{
    res.render('/homepage')
})


2a. // Route properly. In your index.js if you have your routes in a controller, make
sure to route from the index.js to your controller folder

Example in index.js:

let yourControllerConst = require('./controllers/yourfilename');
app.use('/yourfilename', yourControllerConst)

Any other route you can add after the '/' like /about or /blog. 
You can use parameters to access a number of values using ":" for example: app.get('/animal/:name') will match for any route with /animal/SOMETHING and you can access name via the object req.params.name in the callback. Adding the asterisk to a route will match anything after it.

Query strings can also be passing in a path after the question mark. These appear in req.query under key/value pairs https://www.domain.com/some/data?key1=value&key2=value2



---ejs Templates---
1. // After installing the package for ejs, declare these things in your index.js 

You need to run ejs middleware as such:

// This tells express that we'll be using ejs as the view engine
app.set('view engine','ejs')
app.use(ejsLayouts)

Then you need to change your res.sendFile to res.render to tell express to use the ejs.
The files need to all be in a views directory. Using ejs you can send variables (as objects) via the optional second parameter to res.render as key/value pairs. then you can use these variables in the ejs templates to do some JS. The <%= is when you want to return or show a value, and the <% is just when you want to do some logic.

With ejs you can also use partials which are part of a page, like a header or footer. This is a separate .ejs file holding header/footer/etc html and you can inject it into any page using: <%- include('../partials/header.ejs') %>


---Views---
1. Make a 'views' folder inside your project folder

---Layouts---
npm package express-ejs-layouts allows you to use page layouts

1. You need to add this const at the top somewhere in your index.js 

const ejsLayouts = require('express-ejs-layouts')

2. Tell express to use ejs-layouts middleware

app.use(ejsLayouts)

You need to have a file in your views directory called layout.ejs 

3.  HTML:5 in your layout.ejs file and inside the body tag have <%-body %> to inject
the things into the body that will be added through other files in the views folder and it would look like this:

<!DOCTYPE html>
<html>
<head>
  <title>Some Title</title>
</head>
<body>
  <%- body %>
</body>
</html>


---Gitignore---

This will tell github which directories not to track

1. Create a .gitignore file 

touch .gitignore in your terminal and 

2. Type out node_modules and .env ONLY inside the .git ignore


---Environment Variables---

You can keep certain things hidden from your app by putting them in a .env file in your root directory of the project. To use them:
1. Install the node package (npm i dotenv) and require/config it with this at the very top of your index.js :

require('dotenv').config()

2. Variables defined inside your .env file can be accessed via process.env.PORT (for key PORT=8000 this would be 8000)

PORT=8000
API_KEY=abc123 (or whatever your key is)

---Sequelize Setup---

1. npm install pg sequelize to install the required node modules
2. sequelize init will create the config.json, models and migrations directories
3. To create the database enter: sequelize db:create db_name (and db_name is the name of the database you want to create)
4. Then create the models by running: sequelize model:create --name user --attributes firstName:string,lastName:string,age:integer,email:string with whatever table columns and types you want. 

**WINDOWS USERS**
To get things working properly, with anything involving sequelize
Need to enter
Username and Password for SQL shell, and "Dialect": "postgres"


The word after --name will be the name of your model. Running this command will create the js file in your /models directory which you should check.
