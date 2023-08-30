## MEAN STACK DEPLOYMENT TO UBUNTU IN AWS
MEAN stack is a combination of following component 
1. **mongoDB** ( Document database) - stores and allows to retrieve data.
2. **Express** ( Back-end application framework) - makes request to database for reads and writes 
3. **angular** ( Frontend application framework)- Handles client and server requests. 
4. **Node.js** (Javascript runtime environment) - Accepts requests and displays results to end user. 

# The goal of this project is to immplement a simple book register web using MEAN stack. 

** STEP 1 : INSTALL nodejs **

Node.js is a javascript runtime buuilt on chrome's V8 Javascript engine. Node.js is used in this tutorial to set up the Express routes and AngularJS controllers. 

-**Update ubuntu**

*sudo apt update*

<img width="1185" alt="Screenshot 2023-08-30 at 12 11 55" src="https://github.com/kelvinola/Devops-Training/assets/115745653/91f3061b-0914-47a8-b815-a8f82818eef0">

-**Upgrade ubuntu**

*sudo apt upgrade -y*
<img width="1096" alt="Screenshot 2023-08-30 at 12 13 13" src="https://github.com/kelvinola/Devops-Training/assets/115745653/8501f39d-9aca-4b9a-9323-32c2175aa1ae">

-**Add certificates**

*sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates*
<img width="1317" alt="Screenshot 2023-08-30 at 12 14 10" src="https://github.com/kelvinola/Devops-Training/assets/115745653/0c156815-2f73-4d15-b976-b3bbac3cd662">

*curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -*

-**Install NodeJS**

*sudo apt install -y nodejs*
<img width="1087" alt="Screenshot 2023-08-30 at 12 14 42" src="https://github.com/kelvinola/Devops-Training/assets/115745653/99f85ad6-ef43-4eff-98e1-9f0651d798eb"> 

**STEP 2: Install MongoDB** 
MongoDB  stores data in flexible, JSON-like documents. Fields in a database can vary from document to document and data structure can be changed over time. For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.

- Import the public Key used by package management system 

<img width="1336" alt="Screenshot 2023-08-30 at 12 46 08" src="https://github.com/kelvinola/Devops-Training/assets/115745653/94d3fa57-5a1f-41b3-b5b5-df5ea6107653">

<img width="1440" alt="Screenshot 2023-08-30 at 12 53 21" src="https://github.com/kelvinola/Devops-Training/assets/115745653/837ffc73-e2e4-4c98-b786-c982bbfa07ee">

- Create a list file for mongoDB 
** FOR UBUNTU 22.04 **
<img width="1423" alt="Screenshot 2023-08-30 at 12 46 38" src="https://github.com/kelvinola/Devops-Training/assets/115745653/59c20d0f-4509-4999-89ad-51704fbd857f">

Reload Local Packages
*sudo apt-get update*

Install MongoDB
*sudo apt-get install -y mongodb-org*
<img width="1440" alt="Screenshot 2023-08-30 at 17 49 21" src="https://github.com/kelvinola/Devops-Training/assets/115745653/af207bf6-2fe5-4d02-b59e-b8fb8221c8e1">

start and enable theh mongod service 

*sudo systemctl start mongod*

*sudo systemctl enable mongod*

Verify that the service is up and running

sudo systemctl status mongod

<img width="1440" alt="Screenshot 2023-08-30 at 17 51 52" src="https://github.com/kelvinola/Devops-Training/assets/115745653/5b705d0f-0d5e-404e-8170-6564dcadb86e">

Install body-parser package

We need ‘body-parser’ package to help us process JSON files passed in requests to the server.

sudo npm install body-parser
<img width="1422" alt="Screenshot 2023-08-30 at 17 52 36" src="https://github.com/kelvinola/Devops-Training/assets/115745653/b4f6a3d5-a036-4f03-831b-f6f530ad518c">


Create a folder named ‘Books’

mkdir Books && cd Books
In the Books directory, Initialize npm project

npm init
<img width="1440" alt="Screenshot 2023-08-30 at 17 53 38" src="https://github.com/kelvinola/Devops-Training/assets/115745653/ad8407ae-4161-4af8-87c4-8da9296c2111">

Add a file to it named server.js

vi server.js
Copy and paste the web server code below into the server.js file.

var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});

<img width="1440" alt="Screenshot 2023-08-30 at 18 07 16" src="https://github.com/kelvinola/Devops-Training/assets/115745653/f5ae644c-039a-413e-8b7f-4c780385fd8b">

## INSTALL EXPRESS AND SET UP ROUTES TO THE SERVER
**Step 3: Install Express and set up routes to the server** 

Express is a minimal and flexible Node.js web application framework that provides features for web and mobile applications. We will use Express in to pass book information to and from our MongoDB database.

We also will use Mongoose package which provides a straight-forward, schema-based solution to model your application data. We will use Mongoose to establish a schema for the database to store data of our book register.

sudo npm install express mongoose

In ‘Books’ folder, create a folder named apps

*mkdir apps && cd apps*

Create a file named routes.js

*vi routes.js*


Copy and paste the code below into routes.js

<img width="1440" alt="Screenshot 2023-08-30 at 18 15 48" src="https://github.com/kelvinola/Devops-Training/assets/115745653/77897520-7627-46fa-8037-62308d04bdfe">

In the ‘apps’ folder, create a folder named models

*mkdir models && cd models*


Create a file named book.js

*vi book.js*


Copy and paste the code below into ‘book.js’

var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';
mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = mongoose.model('Book', bookSchema);

# Step 4 – Access the routes with AngularJS
AngularJS provides a web framework for creating dynamic views in your web applications. In this tutorial, we use AngularJS to connect our web page with Express and perform actions on our book register.

Change the directory back to ‘Books’

*cd ../..*


Create a folder named public

*mkdir public && cd public*


Add a file named script.js

*vi script.js*


Copy and paste the Code below (controller configuration defined) into the script.js file.

<img width="1440" alt="Screenshot 2023-08-30 at 18 21 17" src="https://github.com/kelvinola/Devops-Training/assets/115745653/cd1de032-ace3-4dcd-a791-b9465cbf749b">

In public folder, create a file named index.html;

*vi index.html*

<img width="1440" alt="Screenshot 2023-08-30 at 18 23 30" src="https://github.com/kelvinola/Devops-Training/assets/115745653/d7fe4caa-c4d9-47ec-b7d5-4eae8eb901e0">

Change the directory back up to Books

*cd ..*


Start the server by running this command:

*node server.js*


The server is now up and running, we can connect it via port 3300. You can launch a separate Putty or SSH console to test what curl command returns locally.

curl -s http://localhost:3300
It shall return an HTML page, it is hardly readable in the CLI, but we can also try and access it from the Internet.

For this – you need to open TCP port 3300 in your AWS Web Console for your EC2 Instance.

<img width="1440" alt="Screenshot 2023-08-30 at 18 26 58" src="https://github.com/kelvinola/Devops-Training/assets/115745653/d7b32ba2-594c-49c6-898d-35a8987a2f76">


<img width="1440" alt="Screenshot 2023-08-30 at 18 29 06" src="https://github.com/kelvinola/Devops-Training/assets/115745653/e0fee759-4670-461f-8eb4-c370f6ed0756">

