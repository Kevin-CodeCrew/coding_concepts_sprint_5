###### Top
[Back to Concepts](README.md) | [Jump to Bottom](#Bottom) | [Resource](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/routes)
## Express Router
A `route` is a section of Express code that associates an HTTP verb (GET, POST, PUT, DELETE, etc.), a URL path/pattern, and a function that is called to handle that pattern for that endpoint.

There are several ways to create routes. including the express.Router middleware. It allows us to group the route handlers for a particular part of a site together and access them using a common route-prefix.

### File Structure
- Directory
    - index.js (entry point file)
    - routes (directory)
        - api.js (router module)

### Using Router
#### entry point file
```JavaScript
let express = require('express');
let app = express();
let port = 8000;

let wiki = require('./routes/wiki');

app.use('/wiki', wiki);

app.listen(port, () => {
    console.log(`Listening on port ${port}`)
});
```
#### router module
```JavaScript
// wiki.js - Wiki route module.

var express = require('express');
var router = express.Router();

// Home page route.
router.get('/', function (req, res) {
  res.send('Wiki home page');
})

// About page route.
router.get('/about', function (req, res) {
  res.send('About this wiki');
})

module.exports = router;
```
###### Bottom
