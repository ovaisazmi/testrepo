# Blocking and Non-Blocking

- Blocking :- A situation where a piece of code stops the execution of the rest of the program until it finishes its task. meantime, the program is `blocked` from doing anything else.

- Non-blocking :- A situation where a piece of code does not stop the execution of the rest of the program while it carries out its task. This means that other code can continue to execute concurrently.

---

# Throughput

Throughput is the `speed` at which `data` can be `transmitted` from one place to another. It is usually measured in `bits` per second , `bytes` per second , or some other unit of data transfer rate. `Higher throughput` means that more data can be transmitted in a shorter amount of time, which is generally considered to be `needed` in applications.

---

# ReadFile and ReadFileSync

ReadFile is an asynchronous function, which means that it doesn't block the execution of the rest of the code while it reads the file. Instead, it takes a callback function as a parameter, and that function is executed once the file has been read. The callback function takes two parameters: an error and data and the contents of the file.

js
const fs = require("fs");

fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) console.log(err);
  console.log(data);
});


ReadFileSync is a synchronous function, which means that it blocks the execution of the rest of the code until the file has been read. It returns the contents of the file can be a string or a buffer.

js
const fs = require("fs");

const data = fs.readFileSync("file.txt", "utf8");
console.log(data);


---

# Network request using http module

We can use the built-in http module to make network requests.

Example:-

js
const http = require("http");

const fs = require("fs");

const server = http.createServer((request, response) => {
  if (request.url === "/") {
    fs.readdir("../assignments", (err, data) => {
      if (err) {
        response.end(err);
      } else {
        response.setHeader("Content-Type", "text/html");
        response.end(`<ul>
                ${data
                  .map((el) => {
                    return `<li><a href="/${el}">/${el}</a></li>`;
                  })
                  .join("")}

                </ul>`);
      }
    });
  } else if (request.url === "/index.js") {
    fs.readFile("./index.js", (err, data) => {
      if (err) {
        response.end(err);
      } else {
        response.end(data);
      }
    });
  } else if (request.url === "/public") {
    fs.readdir("./public", (err, data) => {
      if (err) {
        response.end(err);
      } else {
        response.setHeader("Content-Type", "text/html");
        response.end(`<ul>
                ${data
                  .map((el) => {
                    return `<li><a href="/public/${el}">/${el}</a></li>`;
                  })
                  .join("")}

                </ul>`);
      }
    });
  } else {
    response.end("Invalid Path");
  }
});

server.listen(4500, () => {
  console.log("The server is runns at 4500 port");
});


---

# Web Server without Express

We can create a web server using the built-in http module.

Example:-

js
const http = require("http");

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader("Content-Type", "text/plain");
  res.end("Hello");
});

server.listen(3000, () => {
  console.log("Server running on 8080");
});


---

# Libuv

Libuv is a software library that helps Node.js to work better on different operating systems by providing a consistent way to handle input/output (I/O) operations and other system-level tasks. It allows Node.js to perform many tasks at the same time without slowing down, making it fast and efficient.

---

# Event Loop and its Phases

The event loop is the mechanism that enables asynchronous operations to be performed in a non-blocking way. The event loop has several phases, each of which performs a different task. Here are the different phases of the Node.js event loop:

- Timers: This phase executes timer callbacks scheduled by setTimeout() and setInterval() functions. If no timers are scheduled, the event loop will move to the next phase immediately.

- I/O callbacks: This phase executes I/O callbacks such as stream and socket callbacks that were deferred to the next iteration of the event loop. This phase also executes some types of callbacks related to setImmediate().

- Idle, prepare: This phase is used internally by Node.js and is not typically used in user code.

- Poll: This phase retrieves new I/O events from the operating system's kernel, processes them, and executes I/O callbacks associated with them. If no I/O events are detected in this phase, the event loop will either wait for new events to arrive or continue to the next phase.

- Check: This phase executes callbacks scheduled by setImmediate() functions. This phase runs after the Poll phase, but before any Timers phase.

- Close callbacks: This phase executes close event callbacks, such as socket.on('close', ...).

---

# Timers

Timers are used to execute code at a specific time in the future or after a certain interval has passed. Timers are implemented using the `setTimeout()` and `setInterval()` functions and `clearTimeout()` and `clearInterval()` used to end.

The `setTimeout()` function schedules a function to be executed once after a specified delay (in milliseconds).
Example, a function to be executed after 1 second:

js
const timer = setTimeout(() => {
  console.log("Function executed after 1 second");
}, 1000);

setTimeout(() => {
  clearTimeout(timer);
  console.log("Timer canceled");
}, 3000);


The `setInterval()` function schedules a function to be executed repeatedly after a specified interval (in milliseconds). For example, the following code schedules a function to be executed every 5 seconds:

js
setInterval(() => {
  console.log("Function executed every 5 seconds");
}, 5000);


ON Addition settimeout waits for a certain amount of time and then runs the function but setinterval continously runs function for that particular time

---

# NVM - Node Version manager

NVM is a tool that helps you manage different versions of Node.js on your computer. You can use it to install, switch, and manage different versions of Node.js easily. This is useful when you have different projects that require different versions of Node.js, or if you want to test your code with different versions of node how it performs.

---

# CommonJS

CommonJS is a module format that is used in Node.js. It provides a way to define reusable code as modules, which can be loaded and used in other modules. In CommonJS, you use `require()` to load a module, and `module.exports` or `exports` to define what parts of the module can be used by other modules but in es are a newer standard that was introduced in `ECMAScript` 6 (ES6). They provide a similar way to define reusable code as modules, but with a different syntax. In ES modules, you use `import` to load a module, and `export` to define what parts of the module can be used by other modules.

---

# Crypto

The crypto module provides a set of cryptographic functions that can be used to secure data by encrypting, decrypting, and hashing it. The module provides a wide range of algorithms and functions that can be used to meet different security requirements.

---

# WebSockets

WebSockets is a protocol that enables `real-time communication` between a `client` and a `server` over a `single`, long-lived `connection`. It provides a mechanism for a web server to send data to a client in real-time, without the client having to continuously poll the server for new data.

In traditional web applications, the client sends a request to the server and the server responds with a web page or data. The connection between the client and server is then closed. If the client needs to receive updates or new data from the server, it needs to send another request to the server, which can be slow and inefficient. So,

With WebSockets, the connection between the client and server remains open, allowing for real-time, bidirectional communication between the two. This enables the server to push data to the client as soon as it becomes available, without the client having to make a request for it.

WebSockets are widely used for real-time applications such as chat applications, online gaming, financial trading platforms and real time location tracking.

---

# Microservices

Microservices architecture is a way of designing software where large applications are broken down into `smaller`, self-contained `services`. This makes developing and updating applications easier, safer and faster. Instead of building a large application, developers can build and test small parts of it separately, making the development process faster and more efficient. Microservices also make it easy to scale up or down individual parts of an application as needed, which can save time and resources. Overall, microservices architecture helps developers work more efficiently, build better applications, and get them to market faster.

---

# Express

Express is a web application framework for `Node.js` that provides a set of tools and libraries for building web applications and APIs

A quick overview of how Express works:

- The client sends an HTTP request to the server.
- The server receives the request and goes through some middleware functions.
- Each middleware function can change the request or response object and control the next middleware in the chain using the next function.
- If the middleware function sends a response to the client, the middleware chain is stopped and the response is sent.

Otherwise, the request is passed to the next middleware in the chain.
When the request is processed by all the middleware functions, the server sends a response to the client.

---

# Routes

Routes in web applications are URLs that clients use to access different parts of the application. In Express, routes are defined by HTTP methods and corresponding URL paths. When the client sends an HTTP request to a specific destination, the server executes the appropriate code to resolve the request and responds. Routing is a key component of any web application because it defines the structure and functionality of our application's API.

some of Basic routes are

js
GET, PUT, POST, PATCH, DELETE;


---

# Middleware

Middleware is a functions sits between client and server it checks many things like authentication, authorization of a user. Its a way to add additional functionality to a web application in a modular form. Like adding an additional layer where the client and server can exchange request and response objects. These middleware functions can perform tasks such as analyzing request data, handling errors, and authenticating users. They make code more usable and easier to maintain. Popular middleware libraries in Node.js include Express.js, Koa.js, and Connect.

---

# MVC - Model-View-Controller

MVC means Model-View-Controller. its a Common software architecture patterns/practise used in web development.

In MVC, an application is divided into three related components:

- Model: Model represents the data and business logic of the application. It encapsulates data and provides methods for manipulating and retrieving it.

- View: A view is responsible for providing information and presenting it to the user. This is the user interface of the program.

- Controller: A controller acts as an intermediary between the model and the view. It takes input from the user and updates the model and view accordingly.

---

# Validations

Validations are an important part of web development as they help to ensure that the data entered by the user is correct and meets the required standards.

To implement validations in a web application, we can define the validation rules that performing on client-side and server-side validations. We have to display clear error messages, and thoroughly test the validations. There are also many validation libraries available for web frameworks that can simplify the implementation of validations.

---

# Static routing

Static routing is the process of defining a `route` in a web application that `does not change` and does `not depend` on `user input`. This is different from dynamic routing, which uses parameters in the URL to generate different responses based on the information provided.

Static routing is useful for serving static content such as images, CSS and JavaScript files, and for defining pages that do not change frequently.

Also it is not useful for e-commerce websites where we have to make difrent pages according to products.

---

# Templating engines

Templating engines are used in web development to generate dynamic HTML pages based on data received from the server. Examples are

- EJS (Embedded JavaScript): A simple templating language that allows you to embed JavaScript code in HTML templates.
- Handlebars: A popular templating engine that uses a syntax similar to Mustache. It provides a simple way to create reusable templates and partials.
- Pug (formerly Jade): A high-performance templating engine that uses a syntax similar to HAML.

---

# Session Managment

Sessions are a way to store user-specific information between requests. When a user accesses a website, a session is created and a unique session ID is created. This session ID is then stored in a cookie in the user's browser, which allows the server to identify the user and obtain session information for each subsequent request.

In express.js, you can manage sessions using the middleware provided by the popular express session package. steps to manage a session in Express:

1. Install the express session package: npm install Express-session.

2. Configure the session middleware: You need to configure the session middleware with options like session secret, cookie and storage settings.

js
const session = require("express-session");
const app = express();

app.use(
  session({
    secret: "your-secret-key",
    resave: false,
    saveUninitialized: true,
  })
);


3. Set session data: You can set session data for a user using the req.session object. For example, to set a user ID in the session data:

js
app.get("/login", function (req, res) {
  // For Login user
  req.session.userId = "1234";
  res.send("Logged in successfully");
});


4.  Retrieve session data: You can retrieve session data for a user using the req.session object.

js
app.get("/profile", function (req, res) {
  // Getting user ID from session
  const userId = req.session.userId;
  res.send("User ID: " + userId);
});


5. Destroy session data: You can destroy session data for a user using the req.session.destroy() method. For example, to log out a user:

js
app.get("/logout", function (req, res) {
  // Destroying session data
  req.session.destroy(function (err) {
    if (err) {
      console.error(err);
    } else {
      res.send("Logged out successfully");
    }
  });
});


---

# Manage cookies using Express:

Cookies are small pieces of data stored in the client's browser and sent to the server with each request. Express offers middleware "cookie-checker" that you can use to manage cookies.

### Steps to use the cookie-parser:

Install the package: npm install cookie-parser
Configure middleware: Use app.use(cookieParser()) to configure middleware.
Use the cookie object: the cookie object can be accessed from the request object using req.cookies. You can read and write cookies using properties on the Cookie object.

---

# Common libraries for Express:

Express is a popular web framework for Node.js and has a large ecosystem of libraries and plugins.

Here are some common libraries used with Express:
- Body-parser: A middleware used to parse request bodies.
- Mongoose: A popular library for connecting to and interacting with MongoDB.
- Passport: A middleware used for authentication.
- Morgan: A middleware used for logging HTTP requests.
- Helmet: A middleware used to secure your Express app by setting various HTTP headers.

---

# CORS

CORS stands for Cross-Origin Resource Sharing. A Security features implemented in web browsers to restrict web pages from making requests to other domains that provide original content. CORS helps prevent malicious attacks by limiting access to sensitive data between different origins.

For installing to local machine:-

js
npm install cors



---

# Testing

Testing is the process of evaluating a system or its components with the intent to find whether it satisfies the specified requirements or not. Testing can be done manually or using automated tools, and it is an essential part of software development.

For doing testing we have write parameters and certain conditions where program needs to perform and we also keep in mind of possible edge cases.

---

# Unit testing

Unit testing is a type of testing that focuses on verifying the behavior of individual units or components of a system. In unit testing, each unit is tested separately to ensure that it functions correctly and meets its intended specifications.

---

# Functional testing

Functional testing is a type of testing that focuses on verifying that the functionality of the software meets the specified requirements. In functional testing, the software is tested against a set of expected behaviors or inputs to ensure that it performs as expected.

---

# HTTPS

HTTPS stands for Hypertext Transfer Protocol Secure. It is a protocol for secure communication over the internet. HTTPS is used to encrypt the data that is sent between a web server and a client, making it difficult for unauthorized users to access or intercept sensitive information.

---

# Difference between HTTP and HTTPS

HTTP is a protocol for transferring data over the internet. It is used to transfer information between a web server and a client, such as a web browser. HTTPS is a secure version of HTTP that encrypts the data that is transmitted between the server and client. The main difference between HTTP and HTTPS is that HTTPS uses SSL/TLS encryption to protect the data, whereas HTTP does not.

---

# SSL/TLS

SSL (Secure Sockets Layer) and TLS (Transport Layer Security) are protocols used for securing communication over the internet. They are used to encrypt data that is transmitted between a web server and a client, making it difficult for unauthorized users to access or intercept sensitive information. SSL is an older protocol that has been replaced by TLS, but the term SSL is still commonly used to refer to the encryption process.

---

# OWASP

The Open Web Application Security Project (OWASP) is a non-profit organization founded in 2001, with the goal of helping website owners and security experts protect web applications from cyber attacks. OWASP has 32,000 volunteers around the world who perform security assessments and research.

---

# SQL and NoSQL

### SQL (Structured Query Language)

The Databases are based on a relational model, where data is stored in tables with rows and columns. They are good for handling structured data with well-defined relationships between entities.

### NoSQL (Not only SQL) databases

They do not use tables and rows. Instead, they store data in a variety of ways, including key-value pairs, document-based, or graph-based models. They are more flexible and can handle unstructured or semi-structured data more easily.

---

# Common queries in SQL

Some common SQL queries include

sql
SELECT, INSERT, UPDATE, and DELETE statements.


- SELECT statements are used to retrieve data from a database.
- INSERT statements are used to insert data into a table.
- UPDATE statements are used to modify existing data in a table.
- DELETE statements are used to delete data from a table.

---

# SQL Joins

Joins are used to combine data from two or more tables in a SQL database. There are several types of joins, including

sql
INNER JOIN, LEFT OUTER JOIN, RIGHT OUTER JOIN, and FULL OUTER JOIN.


To perform a join, you need to specify the tables you want to join, the columns to join on, and the type of join you want to perform.

---

# MongoDB $lookup

The $lookup aggregation stage is used to perform a left outer join between two collections. It allows you to combine data from two collections based on a common field. To use $lookup, you need to specify the name of the foreign collection, the local field to join on, the foreign field to join on, and the name of the output field.

---

# CAP theorem

CAP theorem is a concept in distributed systems that states that it is impossible for a distributed system to simultaneously provide all three of the following guarantees

sql
Consistency, Availability and Partition Tolerance.


- Consistency means that all nodes in the system see the same data at the same time.
- Availability means that every request receives a response, without guarantee that it contains the most recent version of the data.
- Partition Tolerance means that the system continues to operate despite arbitrary message loss or network failure between nodes.

According to the CAP theorem, in the presence of a network partition, a distributed system must choose between consistency and availability.

---

# Indexing

Indexing is the process of creating data structures to improve the speed of data retrieval operations on a database. An index is a data structure that provides a quick lookup for a specific value in a database. Indexing can speed up query performance by allowing the database to quickly locate the data that meets the query's criteria.

---

# Database replication

Database replication is the process of copying data from one database to another to create multiple, synchronized copies of the same data. Replication is used to increase data availability and improve scalability and performance of database systems.

---

# PACELC

PACELC is a concept in distributed systems that provides a framework for understanding the trade-off between consistency and availability in the presence of network partitions.

#### PACELC stands for:

- Partition Tolerance: The system continues to function in the event of network partitions.
- Availability: Each request to the system receives a response, without guarantee that it contains
  the most recent version of the data.
- Consistency: All nodes in the system see the same data at the same time.
- Latency: The amount of time it takes for a request to receive a response.
- Efficiency: The amount of resources required to maintain a system.
- Cost: The financial cost of maintaining the system.

---

# Normalization and Denormalization

- Normalization is the process of organizing data in a database to reduce redundancy and dependency. It involves dividing larger tables into smaller tables and defining relationships between them. The goal of normalization is to eliminate data redundancy and ensure data integrity.

- Denormalization, on the other hand, is the process of adding redundant data to a normalized database to improve query performance. Denormalization is useful in situations where read performance is more important than write performance or where complex queries are common.

---

# Entity Relationship (ER) Model

An entity relationship (ER) model is a data modeling technique used to represent data in a database. It consists of three components: entities, attributes, and relationships.

- Entities are objects or concepts in the real world that have unique identities, such as customers or products.
- Attributes are characteristics of an entity, such as a name or address.
- Relationships represent connections between entities, such as customer orders.

ER models are used to design and visualize database structures and communicate requirements to developers and stakeholders.
