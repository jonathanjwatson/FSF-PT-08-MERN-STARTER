# FSF-PT-08-MERN-STARTER

M - MongoDB
E - Express
R - React
N - Node

## Basic Setup

1. `touch server.js`
2. `npm init -y`
3. `npm install express mongoose`

## Build the Express App

1. Require express.
2. Create an instance of express.
3. Set the server PORT to 3001.
4. Listen on the PORT
5. Add middleware

```javascript
app.use(express.urlencoded({ extended: true }));
app.use(express.json());
```

6. Create your routes.

## Add MongoDB/Mongoose to the Server

1. Require mongoose in the server.js
2. Setup the mongoose connection
3. Add mongoose config object to the .connect method.

```javascript
{
  useNewUrlParser: true,
  useUnifiedTopology: true,
  useFindAndModify: false,
  useCreateIndex: true
}
```

4. Optional: include connection.on("error");

## Add React to the App

1. `npx create-react-app client`
2. Add a proxy to the client package.json

```javascript
"proxy": "http://localhost:3001",
```

### Configure a script to run express and react at the same time.

1. cd back into the server root
2. `npm install concurrently if-env`
3. Modify scripts in server package.json

```javascript
    "start": "if-env NODE_ENV=production && npm run start:prod || npm run start:dev",
    "start:prod": "node server.js",
    "start:dev": "concurrently \"nodemon --ignore 'client/*'\" \"npm run client\"",
    "client": "cd client && npm run start",
```

## Deploy App to Heroku

1. `git add .` -> `git commit -m `
2. `heroku create`
3. `git push heroku main`
4. Add three more scripts to the server package.json

```javascript
    "install": "cd client && npm install",
    "build": "cd client && npm run build",
    "heroku-postbuild": "npm run build"
```

5. Require path in server.js
6. Statically server the `client/build` folder.
7. On a final, wildcard route, serve up the index.html from the `client/build` directory.

```javascript
app.use(express.static("client/build"));
```
