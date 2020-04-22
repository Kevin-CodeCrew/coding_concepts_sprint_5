###### Top
[Back to Concepts](README.md) | [Jump to Bottom](#Bottom) 
## Mongo DB + Mongoose
Mongoose is a MongoDB object modeling tool designed to work in an asynchronous environment. Mongoose is by far the most popular ODM, and is a reasonable choice if you're using MongoDB for your database. Mongoose acts as a front end to MongoDB, an open source NoSQL database that uses a document-oriented data model. A “collection” of “documents” in a MongoDB database is analogous to a “table” of “rows” in a relational database.
This ODM and database combination is extremely popular in the Node community, partially because the document storage and query system looks very much like JSON, and is hence familiar to JavaScript developers.
### Mongo Atlas
MongoDB Atlas is the global cloud database service for modern applications. Deploy fully managed MongoDB across AWS, Azure, or GCP. Use MongoDB's robust ecosystem of drivers, integrations, and tools to build faster and spend less time managing your database. We can grab the connection string from Mongo Atlas. We can also view and manage all collections from this client.
### Connecting to the Mongo Database
Mongoose requires a connection to a MongoDB database. You can require() and connect to a locally hosted database with mongoose.connect(), as shown below.
```JavaScript
// CONNECTING TO A MONGO DB DATABASE
// reference the mongoose module 
let mongoose = require('mongoose');
// connect to database
let mongoDB = 'mongodb+srv://USERNAME:PASSWORD@cluster0-ueqkv.mongodb.net/DATABASE_NAME?retryWrites=true&w=majority'
mongoose.connect(mongoDB, {useNewUrlParser: true, useUnifiedTopology: true, useFindAndModify: false});
// connection error message
let db = mongoose.connection;
db.on('error', console.error.bind(console, 'MongoDB connection error:'));
```
### Mongoose Schemas
`Models` are *defined* using the `Schema` interface. The Schema allows you to define the fields stored in each document along with their validation requirements and default values. 
Schemas are then *compiled* into models using the mongoose.model() method. Once you have a model you can use it to find, create, update, and delete objects of the given type.
```JavaScript
//Require Mongoose
let mongoose = require('mongoose');
//Define a schema
let Schema = mongoose.Schema;
// define model
let SomeModelSchema = new Schema({
  a_string: String,
  a_date: Date,
  a_number: Number,
});
// compile model from schema
module.exports = mongoose.model('SomeModel', SomeModelSchema );
```
When you export your model the first argument is the singular name of the collection that will be created for your model (Mongoose will create the database collection in Mongo DB for the above model SomeModel), and the second argument is the schema you want to use in creating the model.
### Manipulating Collection Documents
In order to manipulate your collection you have to require it into the file with the endpoints that need access to it. Typically we will name the required model as a collection.
```JavaScript
let SomeCollection = require('../models/SomeModel');
```
Creation of records (along with updates, deletes, and queries) are asynchronous operations — you supply a callback that is called when the operation completes. The API uses the error-first argument convention, so the first argument for the callback will always be an error value (or null). If the API returns some result, this will be provided as the second argument.
##### Read All
To read all documents in a collection call the `find` method on the collection in a `get endpoint` and pass in an empty filter for the first parameter.
```JavaScript
router.get('/', (req,res) => {
    SomeCollection.find(
        {}, (error, result) => {
            error ? res.send(error) : res.send(result)
        }
    );
});
```
##### Read Some
To read some filtered documents from a collection call the `find` method on the collection in a `get endpoint` and pass in a filter as the first parameter. The filter object has a property name of some property defined in your model to filter by and a property value of some property access dynamically to match. For example the filter `{ role : "instructor" }` would return all documents with the role property value of `instructor`. Typically the property value to match is passed via the path like in the example below.
```JavaScript
router.get('/:property', (req,res) => {
    SomeCollection.find(
        {modelProperty : req.params.property}, (error, result) => {
            error ? res.send(error) : res.send(result)
        }
    );
});
```
##### Read One
To read one filtered document from a collection call the `findOne` method on the collection in a `get endpoint` and pass in a filter as the first parameter. The filter object has a property name of some property defined in your model to filter by and a property value of some property access dynamically to match. For example the filter `{ username : "CoolTechie" }` would return the first document with the username property value of `CoolTechie`. Typically the property value to match is passed via the path like in the example below.
```JavaScript
router.get('/:property', (req,res) => {
    SomeCollection.findOne(
        {modelProperty : req.params.property}, (error, result) => {
            error ? res.send(error) : res.send(result)
        }
    );
});
```
##### Create
To create a document in a collection call the `create` method on the collection in a `post endpoint` and pass in the json object to add to the collection as the first parameter. Typically this object comes from the body of the request via a form submission (or test in postman) so the object can  be accessed by `req.boy`
```JavaScript
router.post('/', (req,res) => {
    SomeCollection.create(
        req.body, (error, result) => {
            error ? res.send(error) : res.send(result)
        }
    );
});
```
##### Update
To update and existing document in a collection call the `findOneAndUpdate` method on the collection in a `put endpoint`. Pass in a filter as the first parameter and pass in the json object to add to the collection as the second parameter. The filter object has a property name of some property defined in your model to filter by and a property value of some property access dynamically to match. For example the filter `{ skillLevel : "expert" }` would return the first document with the skillLevel property value of `expert`. Typically the property value to match is passed via the path like in the example below. Typically the json object comes from the body of the request via a form submission (or test in postman) so the object can  be accessed by `req.boy`
```JavaScript
router.put('/:property', (req,res) => {
    SomeCollection.findOneAndUpdate(
        {modelProperty : req.params.property}, req.body, (error, result) => {
            error ? res.send(error) : res.send(result)
        }
    );
});
```
##### Delete
To read one filtered document from a collection call the `findOneAndDelete` method on the collection in a `delete endpoint` and pass in a filter as the first parameter. The filter object has a property name of some property defined in your model to filter by and a property value of some property access dynamically to match. For example the filter `{ cardNumber : 3456 }` would delete the first document with the cardNumber property value of `3456`. Typically the property value to match is passed via the path like in the example below.
```JavaScript
router.delete('/:property', (req,res) => {
    SomeCollection.findOneAndDelete(
        {modelProperty : req.params.property}, (error, result) => {
            error ? res.send(error) : res.send(result)
        }
    );
});
```
#### Resources
- [MDN Mongoose ODM 1](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose)
- [MDN Mongoose Primer](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose#Mongoose_primer)
- [MDN Mongoose Models](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Express_Nodejs/mongoose#Using_models)
- [Mongoose Models Reference](https://mongoosejs.com/docs/models.html)
- [Mongoose Query Reference](https://mongoosejs.com/docs/queries.html)

[Back to Top](#Top)
###### Bottom