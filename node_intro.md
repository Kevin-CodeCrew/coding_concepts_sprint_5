###### Top
[Back to Concepts](README.md) | [Jump to Bottom](#Bottom) | [Resource](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/Introduction#Hello_Node.js)

## Server Side Development Introduction  
### Node JS
`Node` (or more formally Node.js) is an open-source, cross-platform runtime environment that allows developers to create all kinds of server-side tools and applications in JavaScript. The runtime is intended for use outside of a browser context (i.e. running directly on a computer or server OS). As such, the environment omits browser-specific JavaScript APIs and adds support for more traditional OS APIs including HTTP and file system libraries.
#### Imports
- Create an index.js file
- Generate the package.json file by running `npm init` in the terminal
- Install express and nodemon by running npm install nodemon express in the terminal
#### Pure Node Server
```JavaScript
// Load HTTP module
const http = require("http");

const hostname = "127.0.0.1";
const port = 8000;

// Create HTTP server 
const server = http.createServer((req, res) => {
   // Send the response body "Hello World"
   res.end('Hello World');
});

// Prints a log once the server starts listening
server.listen(port, hostname, () => {
   console.log(`Server running at http://${hostname}:${port}/`);
})
```
#### Express Server
Express is a framework for building web applications on top of Node.js. It simplifies the server creation process that is already available in Node. In case you were wondering, Node allows you to use JavaScript as your server-side language.
```JavaScript
let express = require('express'); // import express using require
let app = express(); // create server

// route for site root
app.get('/', (req, res)=> {
    res.send("This is a server using node and express");
});

// simple route for path localhost:8000/displayName
app.get('/displayName', (req,res) => {
    res.send("My name is Autumn");
});

// allow server to listen on port 8000 and send Listening Message to terminal
app.listen(8000, () => {
    console.log("Listening on port 8000")
});
```
### Postman
Postman is a collaboration platform for API development. Postman's features simplify each step of building an API and streamline collaboration so you can create better APIs—faster. Postman allows you to create, save and test endpoints without a client.

###### Bottom
