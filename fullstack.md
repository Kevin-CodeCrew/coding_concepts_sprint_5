###### Top
[Back to Concepts](README.md) | [Jump to Bottom](#Bottom) 
## Full Stack Development 
##### communicating with the backend from the frontend
<img src=img/mcv_express.png alt="mvc express" width=400px/>

React functions as the `frontend` or the `client` in MERN application. NodeJS + Express function as the `backend` or the server and MongoDB + Mongoose functions as the `database`. In relational to the MVC model illustrated above Mongoose is the `model`, React is the `view` and Express is the `controller`

### Proxy
In order for our front and back end to communicate (when running projects locally) you have to add a proxy to the `package.json` file in your client. Set the path to `http://localhost:PORTNUMBER` the port number will be number your server is listening on
```JavaScript
{
    // add proxy to the end of package.json file
    "proxy" : "http://localhost:5000"
}

```
### Fetch
Using fetch() can be thought of as using a lower level API for performing your needs to return a response from a URI, in other words sans framework or library. fetch was introduced so that developers could more easily make requests to URI's or rest endpoints for applications. In our MERN applications we can `fetch` to endpoints created in the server to preform the specified request at that endpoint. The fetch method preform a `get` request to the specified path by default and any other HTTP method must be specified.
#### Get All
```JSX
// call async fetch
componentDidMount = () => {
    this.loadData();
}
// get all documents from collection
loadData = async () => {
    // fetch from endpoint
    const response = await fetch(`/api`);
    // pull out json data
    const json = await response.json();
    // console.table(json); // check json data returned in console
    // update prop of state with json data from fetch
    this.setState({ cardHolders: json });
}
```
#### Get One
```JSX
// call async fetch
componentDidMount = () => {
    this.loadData();
}
// get all documents from collection
loadData = async () => {
    // fetch from endpoint with query param
    const response = await fetch(`/api/${property}`);
    // pull out json data
    const json = await response.json();
    // console.table(json); // check json data returned in console
    // update prop of state with json data from fetch
    this.setState({ cardHolders: json });
}
```
#### Create
```JSX
// event handler to create document from form submission
handleSubmission = async (event) => {
    event.preventDefault(); // stop page from reloading
    // console.table(this.state); // check current state on submission in console

    // object from form submission to send via fetch
    let formSubmission = {
        cardHolderName: this.state.cardHolderName,
        cardHolderNumber: this.state.cardHolderNumber,
        cardNumber: this.state.cardNumber,
        cardHolderZipCode: this.state.cardHolderZipCode
    }

    // fetch post endpoint
    let response = await fetch('/api', {
        method: "POST",
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
        },
        // send form submission in request body
        body: JSON.stringify(formSubmission)
    });
    // pull out json data
    let json = await response.json();
    // console.log(json); // check returned json data in console
}
```
#### Update One
```JSX
// event handler to update existing document from form submission
handleSubmission = async (event) => {
    event.preventDefault(); // keep page from reloading

    // object for form submission
    let formSubmission = {
        cardHolderName: this.state.cardHolderName,
        cardHolderNumber: this.state.cardHolderNumber,
        cardNumber: this.state.cardNumber,
        cardHolderZipCode: this.state.cardHolderZipCode
    }

    // fetch put endpoint with query params
    let response = await fetch(`/api/${property}`, {
        method: "PUT",
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
        },
        // send form submission in request body
        body: JSON.stringify(formSubmission)
    });
    // pull out json data
    let json = await response.json();
    // console.log(json); // check returned json data
}
```
#### Delete One
```JSX
// event handler when delete button is clicked
handleDeletion = async () => {
    // fetch from delete endpoint with query param
    let response = await fetch(`/api/${property}`, {
        method: "DELETE"
    });
    // pull out json data
    let json = await response.json();
    // console.log(json); // check deleted document in console
}
```
[Back to Top](#Top)
###### Bottom
