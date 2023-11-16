# Express-mongoDB-CRUD-api
Welcome to the Express MongoDB CRUD repository! This project is a hands-on guide to building a web application with basic CRUD (Create, Read, Update, Delete) functionality using Express.js and MongoDB. Whether you're a beginner exploring backend development or an experienced developer looking to reinforce your skills, this repository provides a step-by-step tutorial, code snippets, and best practices.



## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Our Goal](#our-goal)
4. [CRUD in Express](#crud-in-express)
   - [Server Side Development](#server-side-development)
   - [Creating an Express Application](#creating-an-express-application)
   - [Connecting Express with MongoDB](#connecting-express-with-mongodb)
   - [Creating API Endpoints for CRUD](#creating-api-endpoints-for-crud)
5. [CRUD Naming Convention](#crud-naming-convention)



## Introduction
*Express.js is a minimal and flexible web application framework widely used in the Node.js ecosystem to build server-side applications and APIs. It provides a set of features for building web and mobile applications.
 Express.js is known for its simplicity, speed, and the ease with which developers can build RESTful APIs and web applications.
we are going to learn about Basic CRUD in the express. Before getting started with the topic, let us get a short overview of the topic.*

- **Prerequisites**
    - *HTML/ CSS /JS*
- **Our Goal**
    - *Learn CRUD using express and explore the frontend backend and database relationship.*


## Our Goal

Our goal is to guide you through the process of building a basic CRUD (Create, Read, Update, Delete) application using Express.js and MongoDB. By the end of this tutorial, you will have a solid understanding of server-side development with Express, connecting to a MongoDB database, and creating API endpoints to perform CRUD operations. Whether you are a beginner or an experienced developer, this documentation aims to provide a clear and hands-on approach to implementing these fundamental concepts in web development.


## CRUD in Express
*CRUD in ExpressJS refers to the four basic operations of persistent storage: Create, Read, Update, and Delete. These operations are essential in building web applications that interact with a database or any other data source. With ExpressJS, developers can easily implement CRUD functionality by defining routes that handle each operation and interact with the database through an ORM or other data access library. The framework provides a flexible and scalable architecture for building web applications that can handle a high volume of traffic and provide a seamless user experience.*

## Server Side development

- **Introduction to Server-Side Development**

*Server-side development is a critical aspect of web application development, responsible for managing the behind-the-scenes operations that make a website or web application fully functional. In this introductory section, we will explore why server-side development is necessary and how it operates.*

- **Why Server-Side Development is Needed**
    - **Processing Business Logic**
    - **Data Storage and Retrieval**
    - **Security**
    - **Scalability**

-**How Server-Side Development Works**

  - **Client Requests**
  - **Server Receives the Request**
  - **Routing and Processing**
  - **Database Interaction**
  - **Response Generation**
  - **Sending the Response**
  - **Client-Side Interaction**

## Creating An express Application

### Step one: `Importing Required Modules:`
```javascript
const express = require("express");
const cors = require("cors");
```
*Here, you are importing two Node.js modules. express is the module that provides functionality for creating a web server and routing, and cors is a middleware that enables Cross-Origin Resource Sharing (CORS), allowing your server to accept requests from different domains.*

### Step Two: `Creating an Express Application:`

```javascript
const app = express();
```
*This line initializes an instance of the Express application, which you'll use to define routes and handle HTTP requests.*

### Step Three: `Setting the Port:`


```javascript
const port = process.env.PORT || 5001;
```

### Step Four: `Middleware Configuration:`
*These lines configure middleware for your Express application. The `cors()` middleware is used to handle Cross-Origin Resource Sharing, which allows your server to accept requests from different origins. The `express.json()` middleware parses incoming JSON data in request bodies.*

### Step Five: `Defining a Route:`

```javascript
app.get("/", (req, res) => {
  res.send("Crud is running...");
});

```
*This code defines a route for a GET request to the root path `("/")`. When a user accesses the root URL of your server, it responds with the string "Crud is running...". This is a simple example of how you can define routes to handle specific HTTP methods and respond to client requests.*


### Step Six: `Starting the Server:`

```javascript

app.listen(port, () => {
  console.log(`Simple Crud is Running on port ${port}`);
});

```
*This code starts the Express server and makes it listen on the specified port. The app.listen() method starts the server, and the callback function is executed once the server is running. It logs a message indicating that the server is running and listening on a specific port.*

## Connecting Express with MongoDB

### `MongoDB:`
*MongoDB is a popular NoSQL database that stores data in a flexible, JSON-like format called BSON (Binary JSON).*

#### Install MongoDB Node.js Driver:

*You need to install the MongoDB Node.js driver using npm (Node Package Manager)*:
```bash
npm install mongodb

```

### Connecting to MongoDB

```javascript
const express = require("express");
const { MongoClient, ServerApiVersion } = require("mongodb");
const cors = require("cors");
const app = express();

const port = process.env.PORT || 5001;

//  MONGODB DATABASE USER PASSWORD

const uri =
  "mongodb+srv://userName:password@cluster0.cnfykcr.mongodb.net/?retryWrites=true&w=majority";

// Create a MongoClient with a MongoClientOptions object to set the Stable API version
const client = new MongoClient(uri, {
  serverApi: {
    version: ServerApiVersion.v1,
    strict: true,
    deprecationErrors: true,
  },
});

async function run() {
  try {
    // Connect the client to the server	(optional starting in v4.7)
    await client.connect();


    // Send a ping to confirm a successful connection
    await client.db("admin").command({ ping: 1 });
    console.log(
      "Pinged your deployment. You successfully connected to MongoDB!"
    );
  } finally {
    // Ensures that the client will close when you finish/error
    // await client.close();
  }
}
run().catch(console.dir);

app.use(cors());
app.use(express.json());

app.get("/", (req, res) => {
  res.send("Crud is running...");
});

app.listen(port, () => {
  console.log(`Crud is Running on port ${port}`);
});
```
*Replace "your-mongodb-connection-string" with the actual connection string for your MongoDB database.*


# Creating API Endpoints for CRUD

## `POST`
### Client side: 




```javascript 

// using fetch

fetch("http://localhost:5001/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(formData),
    })
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
      });
  };

// using async await 

try {
      const response = await fetch("http://localhost:5001/users", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(formData),
      });
      const result = await response.json();
      console.log(result);
    } catch (error) {
      console.log(error);
    }



// using axios

const axios = require('axios');

try {
  const response = await axios.post("http://localhost:5001/users", formData, {
    headers: {
      'Content-Type': 'application/json',
    },
  });
  console.log(response.data);
} catch (error) {
  console.log(error);
}

```
1. **`fetch("http://localhost:5001/users", ...)`**:
    - This part initiates a network request to the specified URL, "http://localhost:5001/users". It can be any valid URL to a server or API endpoint.

2. **`method: "POST"`**:
    - The **`method`** option specifies the HTTP method for the request. In this case, it's set to "POST," indicating that the request is intended to create or add new data on the server. It's often used to submit data to the server.
3. **`headers: { "Content-Type": "application/json" }`**:
    - The **`headers`** option is an object that defines the HTTP headers for the request. In this case, it specifies that the request is sending data in JSON format. The "Content-Type" header indicates that the request body is formatted as JSON.
4. **`body: JSON.stringify(formData)`**:
    - The **`body`** option is where the actual data that you want to send to the server is defined. It's the request payload. In this line, **`JSON.stringify(formData)`** converts a JavaScript object (in this case, **`formData`**) into a JSON string. The **`formData`** variable should contain the data you want to send to the server, and it will be sent as the request's payload.

So, in summary, this code is making an HTTP POST request to "http://localhost:5001/users" with a request body that contains data in JSON format, as specified by the "Content-Type" header. The server at that URL is expected to handle the request, parse the JSON data, and process it accordingly, such as saving it to a database or performing some other action based on the data provided in the **`formData`** object.

### Server side: 

```javascript
app.post("/users", async (req, res) => {
      const user = req.body;
      //   console.log(user);
      const result = await usersCollection.insertOne(user);
      console.log(result);
      res.send(result);
    });

```

1. **`app.post("/users", async (req, res) => { ... }`**:
    - This code sets up an HTTP POST route using Express. It listens for POST requests at the "/users" URL path. When a client sends a POST request to this endpoint, this route handler will be triggered.

2. **`const user = req.body;`**:
    - In this line, it extracts the data from the request body. When a client sends a POST request, they typically include data in the request body. The **`req.body`** object contains the data sent by the client in JSON format. This line extracts that data and stores it in the **`user`** variable.
3. **`const result = await usersCollection.insertOne(user);`**:
    - This line appears to be using a database operation to insert the **`user`** object (which is typically a user's data) into a database collection. The code is making use of **`await`**, indicating that this operation is asynchronous and may take some time to complete. The actual database operation depends on the framework or library being used. The assumption here is that it's inserting the **`user`** object into a collection (possibly a MongoDB collection) named **`usersCollection`**. The **`result`** variable likely contains information about the outcome of the insertion operation.

4. **`console.log(result);`**:
    - This line logs the **`result`** of the database insertion to the server's console. This is helpful for debugging and monitoring what happened with the database operation.
5. **`res.send(result);`**:
    - Finally, this line sends a response back to the client. It typically sends the result of the database operation back to the client. The **`result`** could include information about the inserted user or an acknowledgment of the successful operation. The client that made the POST request will receive this response.

In summary, this code sets up an Express route to handle HTTP POST requests to the "/users" endpoint. When a POST request is received, it extracts the data from the request body, inserts it into a database collection, logs the result, and sends a response back to the client. This is a common pattern for handling user data submissions and database interactions in a web application.


## `Read`
### Client side: 

```javascript 
fetch("http://localhost:5001/users")
```
- use the **`fetch`** function to make an HTTP GET request to "http://localhost:5001/users."
- you can also use **`axios`** to make an HTTP GET request"


### Server side: 

```javascript
app.get("/users", async (req, res) => {
      const result = await usersCollection.find().toArray();
      res.send(result);
    });
```

1. **`app.get("/users", async (req, res) => { ... });`**:
    - This code sets up a route handler for HTTP GET requests with the path "/users." When a client (such as a web browser or a mobile app) makes a GET request to the "/users" URL on the server, this route handler will be invoked.
2. **`async (req, res) => { ... }`**:
    - This is an anonymous asynchronous function that is used as the route handler. It takes two arguments: **`req`** and **`res`**, which represent the incoming HTTP request and the server's response, respectively.
3. **`const result = await usersCollection.find().toArray();`**:
    - This line of code uses the **`await`** keyword to asynchronously query a MongoDB collection named **`usersCollection`**. It invokes the **`find`** method without any specific criteria, which essentially fetches all documents from the "usersCollection" collection. The result is an array of user documents.
4. **`res.send(result);`**:
    - Once the data is retrieved from the database, it is sent as the response to the client using the **`res.send()`** method. In this case, the **`result`** array (user documents) is sent as the response body. The Express framework will automatically set the appropriate HTTP headers and send the response back to the client.

### `Get single data by id:`

### Server side: 
```javascript
app.get("/users/:id", async (req, res) => {
      const id = req.params.id;
      const query = {
        _id: new ObjectId(id),
      };
      const result = await usersCollection.findOne(query);
      console.log(result);
      res.send(result);
    });
```

1. **`app.get("/users/:id", async (req, res) => { ... });`**:
    - This code defines an HTTP GET route using Express. The route is specified with a path parameter **`:id`**, which is a placeholder for a unique identifier.
    - When a client makes a GET request to a URL like "/users/123" (where "123" is the unique identifier), this route handler is triggered.
2. **`const id = req.params.id;`**:
    - This line retrieves the **`id`** from the URL parameters. In this case, it extracts the **`id`** from the **`req.params`** object. **`req.params`** contains route parameters, and **`id`** corresponds to the **`:id`** parameter in the URL.
3. **`const query = { _id: new ObjectId(id) };`**:
    - This code creates a query object that is used to specify the document to be retrieved. It creates a query based on the **`_id`** field, which is expected to be an ObjectId (typically used for MongoDB).
    - The **`new ObjectId(id)`** part converts the **`id`** obtained from the URL into an ObjectId, which is the type MongoDB uses for unique identifiers.
4. **`const result = await usersCollection.findOne(query);`**:
    - Here, an asynchronous database query is performed on a MongoDB collection named **`usersCollection`**. It uses the **`findOne`** method to find a single document that matches the **`query`** defined earlier.
    - The result of the query (a user document) is stored in the **`result`** variable.
5. **`console.log(result);`**:
    - This line logs the result of the database query to the console. It's typically used for debugging and can show the user data that was retrieved.
6. **`res.send(result);`**:
    - Finally, the result of the database query is sent as a response to the client using **`res.send()`**. This response typically includes the user data as a JSON object, which the client can use.

## `DELETE`

### Client side: 

```javascript

 // delete single data using async await
try {
      const response = await fetch(`http://localhost:5001/users/${_id}`, {
        method: "DELETE",
      });
      const result = await response.json();
      console.log(result);
    } catch (error) {
      console.log(error);
    }

// delete single data using fetch
fetch(`http://localhost:5001/users/${_id}`, {
      method: "DELETE",
    })
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
      });
```
1. **`fetch(`**[http://localhost:5001/users/${_id}`](http://localhost:5001/users/$%7B_id%7D%60), { method: "DELETE" })`:
    - This line initiates an HTTP DELETE request to a URL constructed by interpolating the value of **`_id`** into the URL string. It's assumed that **`_id`** contains a unique identifier for a specific user (or resource) that you want to delete.
    - The **`{ method: "DELETE" }`** option is passed to specify that this is a DELETE request.
2. **`.then((res) => res.json())`**:
    - After the DELETE request is made, this part of the code chains a **`then`** method to handle the response once it is received.
    - **`res`** is the response object. This line is calling **`res.json()`** to parse the response body as JSON. This is typically done if the server is expected to send JSON data in its response.
3. **`.then((data) => { console.log(data); });`**:
    - Once the response has been successfully parsed as JSON, this line uses another **`then`** method to handle the resulting data.
    - The parsed JSON data is stored in the **`data`** variable, and then it's logged to the console using **`console.log`**. This part is often used to process the data received from the server after a DELETE request.

In summary, the code sends an HTTP DELETE request to a URL, likely to delete a user or resource with a specific **`_id`**. Once the request is completed and the server responds, it parses the JSON response data and logs it to the console. This is a common pattern for making DELETE requests to a server and handling the server's response in JavaScript.

### Server side: 
```javascript
app.delete("/users/:id", async (req, res) => {
      const id = req.params.id;
      console.log("delete", id);
      const query = {
        _id: new ObjectId(id),
      };
      const result = await usersCollection.deleteOne(query);
      console.log(result);
      res.send(result);
    });
```

1. **`app.delete("/users/:id", async (req, res) => { ... });`**:
    - This code defines an HTTP DELETE route using Express. The route is specified with a path parameter **`:id`**, which is a placeholder for a unique identifier.
    - When a client makes a DELETE request to a URL like "/users/123" (where "123" is the unique identifier), this route handler is triggered.
2. **`const id = req.params.id;`**:
    - This line retrieves the **`id`** from the URL parameters. In this case, it's extracting the **`id`** from the **`req.params`** object. **`req.params`** contains route parameters, and **`id`** corresponds to the **`:id`** parameter in the URL.
3. **`console.log("delete", id);`**:
    - This line logs a message to the console indicating that a delete operation is being performed and displays the value of **`id`**.
4. **`const query = { _id: new ObjectId(id) };`**:
    - This code creates a query object that is used to specify the document to be deleted. It creates a query based on the **`_id`** field, which is expected to be an ObjectId (typically used for MongoDB).
    - The **`new ObjectId(id)`** part converts the **`id`** obtained from the URL into an ObjectId, which is the type MongoDB uses for unique identifiers.

5. **`const result = await usersCollection.deleteOne(query);`**:
    - Here, it performs an asynchronous delete operation on a MongoDB collection named **`usersCollection`**. It uses the **`deleteOne`** method to delete the document that matches the **`query`** defined earlier.
    - The result of the delete operation is stored in the **`result`** variable.
6. **`console.log(result);`**:
    - This line logs the result of the delete operation to the console. It could be an acknowledgment object indicating how many documents were deleted or any errors encountered during the deletion.
7. **`res.send(result);`**:
    - Finally, the result of the delete operation is sent as a response to the client using **`res.send()`**. This response could be useful for informing the client about the outcome of the delete operation.

## `UPDATE`
### Client side: 
```javacript
fetch(`http://localhost:5001/users/${singledata._id}`, {
      method: "PUT",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ name, password }),
    })
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
      });
```
1. **`fetch("http://localhost:5001/users/${singledata._id}", {...})`**:
    - This line initiates an HTTP PUT request to a URL constructed by interpolating the value of **`singledata._id`** into the URL string. It's assumed that **`singledata._id`** contains the unique identifier of the user you want to update.
2. **`{ method: "PUT", headers: { "Content-Type": "application/json" }, body: JSON.stringify({ name, password }) }`**:
    - Within the options object passed to **`fetch`**, this part of the code specifies various details about the request:
        - **`method: "PUT"`**: Indicates that this is an HTTP PUT request, typically used for updating or replacing a resource on the server.
        - **`headers: { "Content-Type": "application/json" }`**: Sets the request header to indicate that the request body is in JSON format.
        - **`body: JSON.stringify({ name, password })`**: Converts an object with **`name`** and **`password`** properties into a JSON string and sends it as the request body. This object is likely intended to update the user's name and password.
3. **`.then((res) => res.json())`**:
    - After the PUT request is made, this line chains a **`then`** method to handle the response once it is received.
    - **`res`** is the response object. This line is calling **`res.json()`** to parse the response body as JSON. This is typically done if the server is expected to send a JSON response.
4. **`.then((data) => { console.log(data); })`**:
    - Once the response has been successfully parsed as JSON, this line uses another **`then`** method to handle the resulting data.
    - The parsed JSON data is stored in the **`data`** variable, and then it's logged to the console using **`console.log`**. This is often used to process and inspect the data received from the server after the update operation.

### Server side: 
```javascript
app.put("/users/:id", async (req, res) => {
      const id = req.params.id;
      const data = req.body;
      console.log("id", id, data);
      const filter = { _id: new ObjectId(id) };
      const options = { upsert: true };
      const updatedUSer = {
        $set: {
          name: data.name,
          password: data.password,
        },
      };
      const result = await usersCollection.updateOne(
        filter,
        updatedUSer,
        options
      );
      res.send(result);
    });
```
1. **`app.put("/users/:id", async (req, res) => { ... });`**:
    - This code defines an HTTP PUT route using Express. The route is specified with a path parameter **`:id`**, which allows you to update a user with a specific unique identifier.
    - When a client makes a PUT request to a URL like "/users/123" (where "123" is the unique identifier), this route handler is triggered.
2. **`const id = req.params.id;`**:
    - This line retrieves the **`id`** from the URL parameters. In this case, it extracts the **`id`** from the **`req.params`** object, which contains route parameters. **`id`** corresponds to the **`:id`** parameter in the URL.
3. **`const data = req.body;`**:
    - This line extracts the data to be updated from the request's body. The request body should contain the new user information, typically in JSON format. It's assumed that the request body includes fields like **`name`** and **`password`**.
4. **`console.log("id", id, data);`**:
    - This line logs the **`id`** and the updated data to the console for debugging or monitoring purposes.

5. **`const filter = { _id: new ObjectId(id) };`**:
    - This code creates a filter to specify which user to update based on their unique **`_id`**. It constructs the filter using the **`_id`** field and the value extracted from the URL.
6. **`const options = { upsert: true };`**:
    - The **`options`** object is set to **`{ upsert: true }`**. This means that if a user with the specified **`_id`** doesn't exist, a new user will be created with the provided data. If the user already exists, their data will be updated.
7. **`const updatedUser = { $set: { name: data.name, password: data.password } };`**:
    - This code specifies the update operation. It uses the **`$set`** operator to update specific fields, in this case, the **`name`** and **`password`** fields, with the values provided in the request data.

8. **`const result = await usersCollection.updateOne(filter, updatedUser, options);`**:
    - An asynchronous operation is performed on a MongoDB collection named **`usersCollection`**. The **`updateOne`** method is used to apply the update specified in **`updatedUser`** to the user identified by the **`filter`**. The **`options`** indicate whether to create a new document if it doesn't exist.
9. **`res.send(result);`**:
    - Finally, the result of the update operation is sent as a response to the client using **`res.send()`**. The result could be an acknowledgment object indicating how many documents were modified or any errors encountered during the update.


# CRUD naming convention!

1. **Create (POST)**:
    - For creating a new user, use the singular noun "user" and the HTTP POST method.
    - Endpoint: **`/users`**
2. **Read (GET)**:
    - For retrieving one or more users, use the plural noun "users" and the HTTP GET method.
    - Endpoint for getting all users: **`/users`**
    - Endpoint for getting a single user by ID: **`/users/:id`**
3. **Update (PUT)**:
    - For updating a user, use the singular noun "user" and the HTTP PUT method.
    - Endpoint for updating a single user by ID: **`/users/:id`**
4. **Delete (DELETE)**:
    - For deleting a user, use the singular noun "user" and the HTTP DELETE method.
    - Endpoint for deleting a single user by ID: **`/users/:id`**

Here's how the naming convention would look in Express routes using "user" as the resource:

```javascript

const express = require('express');
const app = express();

// Create a new user
app.post('/users', (req, res) => {
  // Create a new user
});

// Get all users
app.get('/users', (req, res) => {
  // Retrieve and return all users
});

// Get a single user by ID
app.get('/users/:id', (req, res) => {
  // Retrieve and return a specific user by ID
});

// Update a single user by ID
app.put('/users/:id', (req, res) => {
  // Update a specific user by ID
});

// Delete a single user by ID
app.delete('/users/:id', (req, res) => {
  // Delete a specific user by ID
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});

```
