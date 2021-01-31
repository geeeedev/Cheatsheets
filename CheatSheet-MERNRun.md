# Purpose: Reminder myself how to get started with a MERN project.

Download and Install

- Visit http://nodejs.org/ and download the latest Long Term Support version (LTS) installation for macOS

Check node version:

```
node -v
```

Enter JavaScript environment:

```
node
```

> Command prompt have now changed from `$` to `>`  
> Everything written will be interpreted as JavaScript

Run a JavaScript file:

```
node nameOfJSFileToBeRun.js
node server.js
nodemon server.js
```

Exit JS env:

```
ctrl C    //(twice)  or  .exit
```

If `node` or `which node` gives an error, use this command to change rights to write files into usr/local:

```
sudo chown -R $(whoami) /usr/local/
```

> NOT recommended with this action - you are changing the ownership of the mac core system - might have bad effects affecting other settings in the long run! Avoid if at all possible! Usually running with prefix `sudo` fixes permission issue.  
> search npm installation re permission for alternate way

Check node location:

```js
which node                           //should give current location of node: usr/local/bin/node
```

## Installing NPM Packages / Dependencies:

- install nodemon globally

  ```js
  npm install -g nodemon          //-g option to install globally to be used anywhere, not project dependent
                                  //might need sudo for macOS
  ```

- install npm package dependencies within a project

  Front-end (react-app client folder)

  ```js
  npm install axios               //install Axios for API (in react-app client folder)
  npm install @reach/router       //install Reach Router for routing (in react-app client folder)
  npm install @material-ui/core   //install Material-UI library for styling (in react-app client folder)
  npm install socket.io-client    //install socket.io (in react-app client folder)
  ```

  Back-end (main project/server side)

  ```js
  npm install cors                //install the ability to make cross-origin requests (backend)
  npm install express             //install Express.js framework for server (backend)
  npm i express                   //short form
  npm install mongoose            //install mongoose for MongoDB (backend)
  npm install socket.io           //install Node.js version Web Sockets API ++ (backend)
  npm install dotenv              //enable the creation of .env hidden file with server.js directory (install within server folder in project)
  npm install jsonwebtoken        //... (backend)
  npm install cookie-parser       //to use cookies in express (backend)
  ```

- install multiple dependencies (eg. express, mongoose) at the same time within a project

  ```js
  npm install express mongoose cors
  ```

- install all dependencies listed in the package.json file within a project

  ```js
  npm install
  ```

- set up a React.js app

  ```js
  npx create-react-app client          //`client` is the folder directory containing this react-app
  ```

- initialize a npm package, such as `react-app` (installed by npx)

  ```js
  npm init react-app client            //same as `npx create-react-app client`
  npm init react-app ./my-react-app
  npm init foo                         //same as `npx create-foo`
  npm init @usr/foo                    //same as `npx @usr/create-foo`
  ```

- start up a legacy npm project with just pacakge.json file created (bare bone)
  ```js
  npm init -y         // without haivng it ask questions
  ```

## Executing app:

- Run React app (in separate console)

  ```
  npm start   OR   npm run start
  ```

- Run server (in separate console)
  ```
  nodemon server.js
  ```

## Installing MongoDB:

- Install using HomeBrew

  ```
  brew tap mongodb/brew
  brew install mongodb-community@4.2
  ```

- Running MongoDB Server (mongod process):
  ```
  brew services start mongodb-community       //replace start with stop to stop
  brew services restart mongodb-community
  ```

- Running Mongo Shell:
  ```mongo
  mongo
  ```

- Test Mongo Running:
  ```js 
  mongo     //start Mongo Shell
  show dbs  //working if see dbs listed
  use <dbName>
  show collections
  quit()     //exit Mongo Shell - "exit" works too
  ```

- Shutting down if mongod window got closed (open new terminal):
  ```mongo
  ps -ax | grep mongo
  ```

- Terminate by process ID:

  > Copy the number (process ID of mongod) on the left of the row that shows `mongo` or `sudo mongo`

  ```mongo
  sudo kill <mongod process ID number>
  ```

- Dropping Mongo Databases

  > This will delete all collections in the database

  ```mongo
  use <mongoDBname>
  use msg_board_db
  db.dropDatabase()       //delete teh current database in use
  ```

- Destroy Mongo Collection (~Table)
  ```mongo
  show collections
  db.<CollectionName>.drop()
  db.userTable.drop()
  db.ninjas.drop()
  ```

## Server Config & Coding:

- directory structure
  - /server:
    - server.js
    - /config
      - mongoose.config.js
    - /controllers
      - \<appName>.controller.js
    - /models
      - \<appName>.models.js
    - /routes
      - \<appName>.routes.js


#### `server.js` - Server Setup
  ```js
  const port = 8000;
  const dbName = "dbFreezer";
  const express = require("express");
  const cors = require("cors");

  //db connection
  require("./config/mongoose.config")(dbName);

  //server
  const app = express();
  app.use(express.json()); //for req.body parsing
  app.use(cors());         //for cross-origin resource sharing (CORS)

  //routes
  require("./routes/freezer.routes")(app);

  //listen
  app.listen(port, () => {
    console.log(`Listing for request on port ${port} to respond to.`);
  });
  ```

#### `mongoose.config.js` - Connection Setup
  ```js
  const mongoose = require("mongoose");

  module.exports = (dbName) => {
    mongoose
      .connect(`mongodb://localhost/${dbName}`, {
        useNewUrlParser: true,
        useUnifiedTopology: true,
        useFindAndModify: false,
      })
      .then((res) => {
        console.log(`Mongoose Config Successfully connected to ${dbName}`);
      })
      .catch((err) => {
        console.log(`Mongoose Config Failed to connect to ${dbName}`, err);
      });
  };
  ```

#### `<>.models.js` - Model & Schema Setup
  ```js
  //create the blueprint to establish model
  const mongoose = require('mongoose');
  const errMsgRequired = "{PATH} is required.";
  const errMsgMinLength = "{PATH} must be at least {MINLENGTH} characters.";

  const FreezerSchema = new mongoose.Schema(
      {
          item: {
              type: String,
              required: [true, errMsgRequired],
              minlength: [3, errMsgMinLength],
          },
          qty: {
              type: String,
              required: [true, errMsgRequired],
          },
          in_date: {
              type: Date,
              required: [true, errMsgRequired],
          },
          out_date: {
              type: Date,
          },
          comment: {
              type: String,
          }
      },
      { timestamps: true}
  );

  //construct model applying schema, then export model
  const Freezer = mongoose.model("Freezer",FreezerSchema);
  module.exports = Freezer;
  ```

#### `<>.controllers.js` - CRUD Control Setup
  ```js
  //establish CRUD control methods using model
  const Freezer = require("../models/freezer.model");

  module.exports = {
    create(req, res) {
      Freezer.create(req.body)
        .then((newItem) => {
          res.json(newItem);
        })
        .catch((err) => {
          res.status(400).json(err);
        });
    },
    getAll(req, res) {
      Freezer.find()
        .then((AllItems) => {
          res.json(AllItems);
        })
        .catch((err) => {
          res.status(400).json(err);
        });
    },
    getOne(req, res) {
      Freezer.findById(req.params.id)
        .then((oneItem) => {
          res.json(oneItem);
        })
        .catch((err) => {
          res.status(400).json(err);
        });
    },
    update(req, res) {
      Freezer.findByIdAndUpdate(req.params.id, req.body, {
        runValidators: true,
        new: true,
      })
        .then((updatedItem) => {
          res.json(updatedItem);
        })
        .catch((err) => {
          res.status(400).json(err);
        });
    },
    delete(req, res) {
      Freezer.findOneAndDelete(req.params.id)
        .then((deletedItem) => {
          res.json(deletedItem);
        })
        .catch((err) => {
          res.status(400).json(err);
        });
    },
  };

  // module.exports = {
  //   create(req, res) {},
  //   getAll(req, res) {},
  //   getOne(req, res) {},
  //   update(req, res) {},
  //   delete(req, res) {},
  // };
  ```

#### `<>.routes.js` - Routing Setup
  ```js
  //establish routing with appropriate controller methods
  const freezerController = require("../controllers/freezer.controller");

  module.exports = (app) => {
      app.post("/api/freezer/new", freezerController.create);
      app.get("/api/freezer", freezerController.getAll);
      app.get("/api/freezer/:id", freezerController.getOne);
      app.put("/api/freezer/:id", freezerController.update);
      app.delete("/api/freezer/:id", freezerController.delete);
      
  };
  ```

- Test this server setup is working with Postman
  - run server
    ```
    cd server
    nodemon server.js
    ```

  - Test with Postman
    - select a request type: GET, POST, PUT, DELETE, etc.
      - do a POST first since we need to add data into the new DB
    - prefix localhost URL based on server port 
      - http://localhost:8000/
    - apply full route based on routes.js setup
      - http://localhost:8000/api/freezer/new
    - prepare data following models.js setup
      - select Body, raw, JSON type
      - ensure JSON formatting
        ```json
        {
          "item":"Bacon",
          "qty":"7 oz",
          "in_date":"2020-05-28",
          "out_date":"",
          "comment":""
        }
        ```
      - click Send button
      - if successful, will receive response with _id (example below)
        ```json
        {
            "_id": "5f1777f3b1b3dd0347367761",
            "item": "Bacon",
            "qty": "7 oz",
            "in_date": "2020-05-28T00:00:00.000Z",
            "out_date": null,
            "comment": "",
            "createdAt": "2020-07-21T23:19:15.567Z",
            "updatedAt": "2020-07-21T23:19:15.567Z",
            "__v": 0
        }
        ```
    - Now do a GET test since we now have data
      - GET
      - http://localhost:8000/api/freezer
      - Send
      - should receive response:
        ```json
        [
            {
                "_id": "5f1777f3b1b3dd0347367761",
                "item": "Bacon",
                "qty": "7 oz",
                "in_date": "2020-05-28T00:00:00.000Z",
                "out_date": null,
                "comment": "",
                "createdAt": "2020-07-21T23:19:15.567Z",
                "updatedAt": "2020-07-21T23:19:15.567Z",
                "__v": 0
            }
        ]
        ```

## Environment Variables:
- react project can consume var declared in your environment (dev,test,prod) as if they were declared locally in your js files.
> Do NOT store secrets (such as private API keys) in your React app!
Environment variables are embedded into the build, meaning anyone can view them by "inspecting" your app's files and network
- create .env file in the root of react project
- store (not-so-secret) keys in .env file
- must prefix all custom variables with `REACT_APP_`
- changing any env var will require a restart of development servier if it is running
- `NODE_ENV` is a react default buildt-in env var
- `NODE_ENV` and REACT_APP_other_env_vars will be defined for you on `process.env`
- REACT_APP_NOT_SECRET_CODE will be exposed in JS as `process.env.REACT_APP_NOT_SECRET_CODE`
- to retrieve variable:
  - `<small>You are running this application in <b>{process.env.NODE_ENV}</b> mode.</small>`
  - npm start: `<small>You are running this application in <b>development</b> mode.</small>`
  - `<input type="hidden" defaultValue={process.env.REACT_APP_NOT_SECRET_CODE} />`
  - npm start: `<input type="hidden" value="abcdef" />`
  - ```js
    if (process.env.NODE_ENV !== 'production') {
      analytics.disable();
    }
    ```
> `NODE_ENV` built-in environment variable (default)  
>- running `npm start`, NODE_ENV = 'development'  
>- running `npm test`,  NODE_ENV = 'test'  
>- running `npm run build`, NODE_ENV = 'production'  *** react production bundle  
>- can never override `NODE_ENV` manually; this is default built-in env var 
>- this prevents developers from accidentally deploying a slow development build to production



- [adding custom env variable](https://create-react-app.dev/docs/adding-custom-environment-variables/)
- [env variable still not secure enough](https://forum.freecodecamp.org/t/keeping-api-key-hidden-using-react/272539)
- [use backend to secure API key in react](https://www.rockyourcode.com/secret-keys-in-react/) - research how to do this (JWToken?)
- [hide secret API keys](https://github.com/react-boilerplate/react-boilerplate/issues/1744#issuecomment-303112505)