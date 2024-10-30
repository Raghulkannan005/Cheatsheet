# Detailed Node.js Course Cheatsheet

## 1. Start Here

- Node.js: JavaScript runtime built on Chrome's V8 JavaScript engine
- Key concepts:
  - Non-blocking I/O
  - Event-driven architecture
  - JavaScript on the server-side

## 2. Read and Write Files

- File System (fs) module:

  ```javascript
  const fs = require('fs');

  // Read file synchronously
  const data = fs.readFileSync('file.txt', 'utf8');

  // Read file asynchronously
  fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
  });

  // Write file synchronously
  fs.writeFileSync('newFile.txt', 'Hello, World!');

  // Write file asynchronously
  fs.writeFile('newFile.txt', 'Hello, World!', (err) => {
    if (err) throw err;
    console.log('File written successfully');
  });
  ```

## 3. NPM Modules

- NPM: Node Package Manager
- Initialize a new project: `npm init`
- Install a package: `npm install package-name`
- Install dev dependency: `npm install package-name --save-dev`
- Update package.json scripts:

  ```json
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  }
  ```

## 4. Event Emitter

- Built-in module for handling events:

  ```javascript
  const EventEmitter = require('events');

  class MyEmitter extends EventEmitter {}

  const myEmitter = new MyEmitter();

  myEmitter.on('event', () => {
    console.log('Event occurred!');
  });

  myEmitter.emit('event');
  ```

## 5. Build a Web Server

- Using the built-in http module:

  ```javascript
  const http = require('http');

  const server = http.createServer((req, res) => {
    res.statusCode = 200;
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello World');
  });

  server.listen(3000, () => {
    console.log('Server running on port 3000');
  });
  ```

## 6. Intro to Express JS framework

- Install Express: `npm install express`
- Basic Express server:

  ```javascript
  const express = require('express');
  const app = express();
  const PORT = 3000;

  app.get('/', (req, res) => {
    res.send('Hello World!');
  });

  app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
  });
  ```

## 7. Middleware

- Middleware functions have access to request and response objects
- Basic middleware:

  ```javascript
  app.use((req, res, next) => {
    console.log(`${req.method} ${req.path}`);
    next();
  });
  ```

- Error-handling middleware:

  ```javascript
  app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Something broke!');
  });
  ```

## 8. Routing

- Basic routing:

  ```javascript
  app.get('/', (req, res) => {
    res.send('Home Page');
  });

  app.post('/users', (req, res) => {
    res.send('Create User');
  });
  ```

- Route parameters:

  ```javascript
  app.get('/users/:id', (req, res) => {
    res.send(`User ${req.params.id}`);
  });
  ```

## 9. MVC REST API

- Model: Data and business logic
- View: Presentation layer (not always used in APIs)
- Controller: Handles requests, interacts with Model
- Example structure:

  ```javascript
  /models
    user.js
  /controllers
    userController.js
  /routes
    userRoutes.js
  ```

## 10. Authentication

- Using Passport.js for authentication:

  ```javascript
  const passport = require('passport');
  const LocalStrategy = require('passport-local').Strategy;

  passport.use(new LocalStrategy(
    (username, password, done) => {
      User.findOne({ username: username }, (err, user) => {
        if (err) { return done(err); }
        if (!user) { return done(null, false); }
        if (!user.verifyPassword(password)) { return done(null, false); }
        return done(null, user);
      });
    }
  ));
  ```

## 11. JWT Auth

- JSON Web Tokens for stateless authentication
- Using jsonwebtoken package:

  ```javascript
  const jwt = require('jsonwebtoken');

  // Create token
  const token = jwt.sign({ userId: user.id }, 'secret_key', { expiresIn: '1h' });

  // Verify token
  jwt.verify(token, 'secret_key', (err, decoded) => {
    if (err) {
      return res.status(401).json({ message: 'Invalid token' });
    }
    req.userId = decoded.userId;
    next();
  });
  ```

## 12. User Roles | Authorization

- Implement role-based access control:

  ```javascript
  const authorize = (role) => {
    return (req, res, next) => {
      if (req.user.role !== role) {
        return res.status(403).json({ message: 'Access denied' });
      }
      next();
    };
  };

  app.get('/admin', authorize('admin'), (req, res) => {
    res.send('Admin page');
  });
  ```

## 13. Intro to MongoDB & Mongoose

- MongoDB: NoSQL database
- Mongoose: ODM (Object Data Modeling) library for MongoDB and Node.js
- Connect to MongoDB:

  ```javascript
  const mongoose = require('mongoose');

  mongoose.connect('mongodb://localhost/myapp', {
    useNewUrlParser: true,
    useUnifiedTopology: true
  });
  ```

## 14. Mongoose Data Models

- Define a schema and model:

  ```javascript
  const mongoose = require('mongoose');

  const userSchema = new mongoose.Schema({
    name: String,
    email: { type: String, required: true, unique: true },
    age: Number
  });

  const User = mongoose.model('User', userSchema);

  module.exports = User;
  ```

## 15. Async CRUD Operations

- Create:

  ```javascript
  const newUser = new User({ name: 'John', email: 'john@example.com', age: 30 });
  await newUser.save();
  ```

- Read:

  ```javascript
  const users = await User.find();
  const user = await User.findById(id);
  ```

- Update:

  ```javascript
  await User.updateOne({ _id: id }, { $set: { name: 'Jane' } });
  ```

- Delete:

  ```javascript
  await User.deleteOne({ _id: id });
  ```
