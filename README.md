# hackathon-visibility-kit

JSAT PRACTICALS — CODE + VIVA QUICK COPY SHEET

PRACTICAL 1 — HELLO WORLD USING HTML AND JAVASCRIPT

<!DOCTYPE html>
Hello World
Hello World
VIVA Q: What is HTML? A: HyperText Markup Language; it structures
webpages. Q: What is JavaScript? A: A programming language used to make
webpages interactive. Q: What does script do? A: It contains or loads
JavaScript. Q: alert()? A: Displays a popup message. Q: console.log()?
A: Prints information to the console.

PRACTICAL 2 — SIMPLE CALCULATOR

<!DOCTYPE html>
Simple Calculator
VIVA Q: What is %? A: Modulus operator; returns the remainder. Q: let?
A: Declares a block-scoped variable that can be reassigned. Q: const? A:
Declares a block-scoped binding that cannot be reassigned. Q: Difference
between / and %? A: / gives quotient; % gives remainder.

PRACTICAL 3 — CONTROL STRUCTURES AND FUNCTIONS

<!DOCTYPE html>
Control Structures and Functions
VIVA Q: if-else? A: Conditional decision-making statement. Q: switch? A:
Selects a matching case based on a value. Q: Why break? A: Prevents
execution from falling through to the next case. Q: Function? A:
Reusable block of code. Q: Arrow function? A: Shorter syntax for writing
functions.

PRACTICAL 4 — TO-DO LIST USING DOM

<!DOCTYPE html>
To-Do List
My To-Do List
Add Task
VIVA Q: DOM? A: Document Object Model; represents HTML as objects
JavaScript can manipulate. Q: getElementById()? A: Selects an element by
its ID. Q: .value? A: Reads an input’s current value. Q: innerHTML? A:
Reads or changes an element’s HTML content. Q: push()? A: Adds an item
to the end of an array. Q: splice()? A: Adds/removes array elements;
here it removes a task.

PRACTICAL 5 — INTERACTIVE CALCULATOR USING DOM

<!DOCTYPE html>
Interactive Calculator
Interactive Calculator
7 8 9 / 4 5 6 * 1 2 3 - 0 . = + C

VIVA Q: DOM manipulation? A: Changing/interacting with HTML elements
using JavaScript. Q: eval()? A: Evaluates a JavaScript expression
represented as a string. Q: Event? A: An action such as clicking or
typing. Q: onclick? A: Runs code when an element is clicked.

PRACTICAL 6 — BASIC HTTP SERVER USING NODE.JS

const http = require(“http”);

const server = http.createServer((req, res) => { res.writeHead(200,
{“Content-Type”: “text/html”}); res.end(“
Hello from Node.js HTTP Server
“); });

const PORT = 3000; server.listen(PORT, () => {
console.log(Server running at http://localhost:${PORT}); });

RUN: node server.js

VIVA Q: Node.js? A: JavaScript runtime that runs JavaScript outside the
browser. Q: http module? A: Built-in module for creating HTTP servers.
Q: createServer()? A: Creates an HTTP server. Q: listen(3000)? A: Starts
listening on port 3000.

PRACTICAL 7 — EXPRESS WEB SERVER WITH MULTIPLE ROUTES

const express = require(“express”); const app = express();

app.get(“/”, (req, res) => { res.send(“
Welcome to my website
“); }); app.get(”/about”, (req, res) => { res.send(“
This is the About page
“); }); app.get(”/services”, (req, res) => { res.send(“
This is the Services page
“); }); app.get(”/contact”, (req, res) => { res.send(“
Contact us at example@gmail.com
“); });

app.listen(3000, () => { console.log(“Server running on
http://localhost:3000”); });

RUN: npm init -y npm install express node app.js

VIVA Q: Express? A: Web framework for Node.js. Q: Routing? A: Defining
responses for URL paths and HTTP methods. Q: app.get()? A: Defines a
handler for GET requests. Q: req and res? A: Request and response
objects.

PRACTICAL 8 — REST API FOR BOOKS

const express = require(“express”); const app = express();
app.use(express.json());

let books = [ {id: 1, name: “The World of Death”, author: “George
Orwell”}, {id: 2, name: “The Way of Death”, author: “John Doe”}, {id: 3,
name: “The Theory of Death”, author: “Someone”}];

app.get(“/books”, (req, res) => { res.status(200).json({ success: true,
data: books, message: “Books fetched successfully” }); });

app.get(“/books/:id”, (req, res) => { const id = Number(req.params.id);
const book = books.find(book => book.id === id);

    if (!book) {
        return res.status(404).json({
            success: false, message: "No Book Found"
        });
    }
    res.status(200).json({
        success: true, data: book,
        message: "Book fetched successfully"
    });

});

app.post(“/books”, (req, res) => { const newBook = {id: books.length +
1, …req.body}; books.push(newBook); res.status(201).json({ success:
true, data: newBook, message: “Book inserted successfully” }); });

app.put(“/books/:id”, (req, res) => { const id = Number(req.params.id);
const book = books.find(book => book.id === id);

    if (!book) {
        return res.status(404).json({
            success: false, message: "No Book Found"
        });
    }
    Object.assign(book, req.body);
    res.status(200).json({
        success: true, data: book,
        message: "Book updated successfully"
    });

});

app.delete(“/books/:id”, (req, res) => { const id =
Number(req.params.id); const index = books.findIndex(book => book.id ===
id);

    if (index === -1) {
        return res.status(404).json({
            success: false, message: "No Book Found"
        });
    }
    const deletedBook = books.splice(index, 1);
    res.status(200).json({
        success: true, data: deletedBook[0],
        message: "Book deleted successfully"
    });

});

app.listen(3000, () => { console.log(“Server running on
http://localhost:3000”); });

VIVA Q: REST API? A: API exposing resources through URLs and HTTP
methods. Q: CRUD? A: Create, Read, Update, Delete. Q: req.params.id? A:
ID from a route parameter, e.g. /books/1. Q: req.body? A: Data sent in
the request body. Q: express.json()? A: Parses incoming JSON request
bodies.

PRACTICAL 9 — MONGODB USER CRUD USING MONGOOSE

const express = require(“express”); const mongoose =
require(“mongoose”); const app = express(); app.use(express.json());

const MONGO_URL = “mongodb://127.0.0.1:27017/usersdb”;

mongoose.connect(MONGO_URL) .then(() => console.log(“Connected to
MongoDB”)) .catch(error => console.log(error));

const userSchema = new mongoose.Schema({ name: String, email: String,
age: Number }); const User = mongoose.model(“User”, userSchema);

app.post(“/users”, async (req, res) => { try { const user = await
User.create(req.body); res.status(201).json({ success: true, data: user,
message: “User inserted successfully” }); } catch(error) {
res.status(500).json({ success: false, message: error.message }); } });

app.get(“/users”, async (req, res) => { try { const users = await
User.find(); res.status(200).json({ success: true, data: users, message:
“Users fetched successfully” }); } catch(error) { res.status(500).json({
success: false, message: error.message }); } });

app.get(“/users/:id”, async (req, res) => { try { const user = await
User.findById(req.params.id); if (!user) { return res.status(404).json({
success: false, message: “User not found” }); } res.status(200).json({
success: true, data: user, message: “User fetched successfully” }); }
catch(error) { res.status(500).json({ success: false, message:
error.message }); } });

app.put(“/users/:id”, async (req, res) => { try { const user = await
User.findByIdAndUpdate( req.params.id, req.body, {new: true} ); if
(!user) { return res.status(404).json({ success: false, message: “User
not found” }); } res.status(200).json({ success: true, data: user,
message: “User updated successfully” }); } catch(error) {
res.status(500).json({ success: false, message: error.message }); } });

app.delete(“/users/:id”, async (req, res) => { try { const user = await
User.findByIdAndDelete(req.params.id); if (!user) { return
res.status(404).json({ success: false, message: “User not found” }); }
res.status(200).json({ success: true, message: “User deleted
successfully” }); } catch(error) { res.status(500).json({ success:
false, message: error.message }); } });

app.listen(3000, () => console.log(“Server running on port 3000”));

VIVA Q: MongoDB? A: NoSQL document-oriented database. Q: Mongoose? A:
ODM library for Node.js and MongoDB. Q: Schema? A: Defines document
fields and their types. Q: Model? A: Interface for interacting with a
collection. Q: User.find()? A: Retrieves matching user documents. Q:
User.create()? A: Creates a document.

PRACTICAL 10 — CENTRALIZED REQUEST LOGGER MIDDLEWARE

const express = require(“express”); const app = express();

const logger = (req, res, next) => { const log =
${new Date().toISOString()} - + ${req.method} ${req.url};
console.log(log); next(); };

app.use(logger);

app.get(“/users/:id”, (req, res) => {
res.send(User details for ID: ${req.params.id}); });

app.get(“/product/:category/:id”, (req, res) => { res.send(
Product category: ${req.params.category}, + Product ID: ${req.params.id}
); });

app.get(“/error”, (req, res) => { res.status(500).send(“Something broke
on the server”); });

app.listen(3000, () => { console.log(“Server is running on port 3000”);
});

VIVA Q: Middleware? A: Function that runs during the request-response
cycle. Q: Middleware parameters? A: req, res, next. Q: next()? A: Passes
control to the next middleware/handler. Q: Why logging middleware? A: To
monitor requests and help debugging.

PRACTICAL 11 — FETCH API

<!DOCTYPE html>
Fetch API Demo
Fetch API Demo
Load Users
VIVA Q: Fetch API? A: Used to make HTTP requests from JavaScript. Q:
fetch() returns? A: A Promise that resolves to a Response. Q:
response.json()? A: Parses the response body as JSON. Q: Promise? A:
Represents the eventual result of an asynchronous operation. Q: Why
check response.ok? A: Fetch does not automatically reject for HTTP error
statuses.

PRACTICAL 12 — SOCKET.IO CHAT

SERVER (server.js)

const express = require(“express”); const http = require(“http”); const
{ Server } = require(“socket.io”);

const app = express(); const server = http.createServer(app); const io =
new Server(server);

app.get(“/”, (req, res) => { res.sendFile(__dirname + “/index.html”);
});

io.on(“connection”, (socket) => { console.log(“New user connected”);

    socket.on("chat message", (msg) => {
        console.log("Message:", msg);
        io.emit("chat message", msg);
    });

    socket.on("disconnect", () => {
        console.log("User disconnected");
    });

});

server.listen(3000, () => { console.log(“Server running on
http://localhost:3000”); });

CLIENT (index.html)

<!DOCTYPE html>
Simple Chat
Chat Application
Send

VIVA Q: Socket.IO? A: Library for real-time, bidirectional client-server
communication. Q: connection? A: Event fired when a client connects. Q:
socket.on()? A: Listens for an event. Q: socket.emit()? A: Sends an
event from a socket. Q: io.emit()? A: Broadcasts to all connected
clients. Q: disconnect? A: Event indicating a client disconnected.

PRACTICAL 13 — UNIT TESTING USING MOCHA

const assert = require(“assert”);

function add(a, b) { return a + b; }

before(function() { console.log(“Before all tests”); });

beforeEach(function() { console.log(“Before each test”); });

afterEach(function() { console.log(“After each test”); });

after(function() { console.log(“After all tests”); });

describe(“Addition Function”, function() { it(“should return 5 when
adding 2 and 3”, function() { assert.strictEqual(add(2, 3), 5); });

    it("should increase by 1", function() {
        let count = 5;
        count = count + 1;
        assert.strictEqual(count, 6);
    });

    it("should increase by 2", function() {
        let count = 5;
        count = count + 2;
        assert.strictEqual(count, 7);
    });

});

RUN: npm install mocha npx mocha

VIVA Q: Mocha? A: JavaScript testing framework. Q: describe()? A: Groups
related tests. Q: it()? A: Defines an individual test case. Q: assert?
A: Checks whether actual output matches expected output. Q: before()? A:
Runs once before tests in its scope. Q: after()? A: Runs once after
tests in its scope. Q: beforeEach()? A: Runs before each test. Q:
afterEach()? A: Runs after each test.

PRACTICAL 14 — GIT

git init git config –global user.name “Your Name” git config –global
user.email “your@email.com” git status git add . git commit -m “First
commit” git remote add origin https://github.com/username/repository.git
git push -u origin main

VIVA Q: Git? A: Distributed version control system. Q: GitHub? A:
Platform for hosting Git repositories and collaboration. Q: git init? A:
Initializes a repository. Q: git add .? A: Stages changes. Q: git
commit? A: Records staged changes in the local repository. Q: Does
commit upload to GitHub? A: No. git push uploads commits to the remote.
Q: git status? A: Shows working tree and staging status. Q: git remote
add origin? A: Adds a remote repository. Q: git push? A: Uploads local
commits to the remote repository.

GENERAL VIVA QUICK REVISION

1.  HTML = webpage structure.
2.  CSS = webpage styling.
3.  JavaScript = webpage behavior.
4.  DOM = object representation of HTML.
5.  Node.js = JavaScript runtime outside browser.
6.  Express = Node.js web framework.
7.  API = interface for software communication.
8.  REST = resource-based API style using HTTP.
9.  CRUD = Create, Read, Update, Delete.
10. GET = read; POST = create; PUT = update; DELETE = delete.
11. MongoDB = NoSQL document database.
12. Mongoose = ODM for MongoDB.
13. Middleware = request-response cycle function.
14. next() = continue to next middleware/handler.
15. Fetch = make HTTP requests.
16. Promise = eventual async result.
17. Socket.IO = real-time communication.
18. Mocha = test framework.
19. Git = version control.
20. Commit = local snapshot.
21. Push = upload commits to remote.
22. Staging area = selected changes prepared for commit.
23. req.params = URL path parameters.
24. req.query = URL query-string values.
25. req.body = request body data.

NOTE This is a clean, runnable study transcription based on the code and
topics previously assembled from the practical file, not a guaranteed
verbatim transcription of every handwritten line in the PDF. Check your
original practical if exact wording, sample values, or formatting is
required.
BRO YES. **Copy this whole answer into Notes/Word right now.** I’ve organized it **Practical-wise exactly according to your PDF**, with the **code + likely viva questions immediately underneath**.

⚠️ **Important reality check:** your PDF is handwritten, so a few characters/lines are difficult to read perfectly. I’m preserving the programs and structure from the PDF, but I’m making obvious syntax/formatting corrections where needed so you can actually copy/run them.

---

# JSAT PRACTICALS — CODE + VIVA

---

# PRACTICAL 1 — Hello World using HTML and JavaScript

### Code

```html
<!DOCTYPE html>
<html>
<head>
    <title>Hello World</title>
</head>

<body>
    <h1>Hello World</h1>

    <script>
        alert("Hello, this is JavaScript!");
        console.log("Hello from JavaScript!");
    </script>
</body>
</html>
```

### Viva

**Q. What is HTML?**
HTML stands for HyperText Markup Language. It is used to structure webpages.

**Q. What is JavaScript?**
JavaScript is a programming language used to make webpages interactive and dynamic.

**Q. What does `<script>` do?**
It is used to write or include JavaScript code in HTML.

**Q. What does `alert()` do?**
It displays a popup message.

**Q. What does `console.log()` do?**
It prints output in the browser/Node console.

---

# PRACTICAL 2 — Simple Calculator

### Code

```html
<!DOCTYPE html>
<html>
<head>
    <title>Simple Calculator</title>
</head>

<body>

<script>
    let num1 = 10;
    let num2 = 5;

    const addition = num1 + num2;
    const subtraction = num1 - num2;
    const multiplication = num1 * num2;
    const division = num1 / num2;
    const remainder = num1 % num2;

    console.log("Addition:", addition);
    console.log("Subtraction:", subtraction);
    console.log("Multiplication:", multiplication);
    console.log("Division:", division);
    console.log("Remainder:", remainder);
</script>

</body>
</html>
```

### Viva

**Q. What is `%`?**
Modulus operator. It returns the remainder.

**Q. What is `let`?**
It declares a block-scoped variable.

**Q. What is `const`?**
It declares a block-scoped variable whose binding cannot be reassigned.

**Q. What is the difference between `/` and `%`?**
`/` gives the quotient. `%` gives the remainder.

---

# PRACTICAL 3 — Control Structures and Functions

### Code

```html
<!DOCTYPE html>
<html>
<head>
    <title>Control Structures and Functions</title>
</head>

<body>

<script>

let marks = 75;

if (marks >= 75) {
    console.log("Excellent");
}
else if (marks >= 60) {
    console.log("Good");
}
else {
    console.log("Need Improvement");
}


// Switch case

let fruit = "apple";

switch (fruit) {

    case "apple":
        console.log("It is an apple");
        break;

    case "banana":
        console.log("It is a banana");
        break;

    default:
        console.log("Unknown fruit");
}


// Regular function

function add(a, b) {
    return a + b;
}

console.log("Addition:", add(10, 20));


// Arrow function

const multiply = (a, b) => a * b;

console.log("Multiplication:", multiply(4, 3));

</script>

</body>
</html>
```

### Viva

**Q. What is an `if-else` statement?**
It is used for conditional decision making.

**Q. What is a switch statement?**
It executes code based on matching a value with different cases.

**Q. Why do we use `break`?**
To stop execution from continuing into the next case.

**Q. What is a function?**
A reusable block of code that performs a particular task.

**Q. What is an arrow function?**
A shorter syntax for writing functions.

---

# PRACTICAL 4 — To-Do List using JavaScript and DOM

### Code

```html
<!DOCTYPE html>
<html>
<head>
    <title>To-Do List</title>
</head>

<body>

<h2>My To-Do List</h2>

<input type="text" id="taskInput"
       placeholder="Enter task">

<button onclick="addTask()">Add Task</button>

<ul id="taskList"></ul>

<script>

let tasks = [];

function addTask() {

    let input = document.getElementById("taskInput");
    let task = input.value;

    if (task === "") {
        alert("Please enter a task");
        return;
    }

    tasks.push(task);

    input.value = "";

    alert("Task added successfully");

    displayTasks();
}


function displayTasks() {

    let taskList = document.getElementById("taskList");

    taskList.innerHTML = "";

    tasks.forEach(function(task, index) {

        let li = document.createElement("li");

        let taskText = document.createElement("span");
        taskText.textContent = task;

        let completeButton =
            document.createElement("button");

        completeButton.textContent = "Complete";

        completeButton.onclick = function() {
            taskText.style.textDecoration = "line-through";
        };

        let deleteButton =
            document.createElement("button");

        deleteButton.textContent = "Delete";

        deleteButton.onclick = function() {
            tasks.splice(index, 1);
            displayTasks();
        };

        li.appendChild(taskText);
        li.appendChild(completeButton);
        li.appendChild(deleteButton);

        taskList.appendChild(li);
    });
}

</script>

</body>
</html>
```

### Viva

**Q. What is DOM?**
DOM stands for Document Object Model. It represents the HTML document as objects that JavaScript can manipulate.

**Q. What does `getElementById()` do?**
It selects an HTML element using its ID.

**Q. What does `.value` do?**
It gets the current value of an input element.

**Q. What does `.innerHTML` do?**
It gets or changes the HTML content inside an element.

**Q. What does `push()` do?**
It adds an element to the end of an array.

**Q. What does `splice()` do?**
It can add/remove elements from an array. Here it is used to delete a task.

---

# PRACTICAL 5 — Interactive Calculator using DOM

### Code

```html
<!DOCTYPE html>
<html>
<head>
    <title>Interactive Calculator</title>
</head>

<body>

<h2>Interactive Calculator</h2>

<input type="text" id="display" readonly>

<br><br>

<button onclick="handleClick('7')">7</button>
<button onclick="handleClick('8')">8</button>
<button onclick="handleClick('9')">9</button>
<button onclick="handleClick('/')">/</button>

<br>

<button onclick="handleClick('4')">4</button>
<button onclick="handleClick('5')">5</button>
<button onclick="handleClick('6')">6</button>
<button onclick="handleClick('*')">*</button>

<br>

<button onclick="handleClick('1')">1</button>
<button onclick="handleClick('2')">2</button>
<button onclick="handleClick('3')">3</button>
<button onclick="handleClick('-')">-</button>

<br>

<button onclick="handleClick('0')">0</button>
<button onclick="handleClick('.')">.</button>
<button onclick="calculate()">=</button>
<button onclick="handleClick('+')">+</button>

<br>

<button onclick="clearDisplay()">C</button>

<script>

let expression = "";

function handleClick(value) {

    expression += value;

    document.getElementById("display").value =
        expression;
}


function calculate() {

    try {

        let result = eval(expression);

        document.getElementById("display").value =
            result;

        expression = result.toString();

    }
    catch(error) {

        document.getElementById("display").value =
            "Error";

        expression = "";
    }
}


function clearDisplay() {

    expression = "";

    document.getElementById("display").value = "";
}

</script>

</body>
</html>
```

### Viva

**Q. What is DOM manipulation?**
Changing or interacting with HTML elements using JavaScript.

**Q. What is `eval()`?**
It evaluates a JavaScript expression represented as a string.

**Q. What is an event?**
An action such as clicking a button or typing.

**Q. What is `onclick`?**
It executes code when an element is clicked.

---

# PRACTICAL 6 — Basic HTTP Server using Node.js

### Code

```javascript
const http = require("http");

const server = http.createServer((req, res) => {

    res.writeHead(200, {
        "Content-Type": "text/html"
    });

    res.end("<h1>Hello from Node.js HTTP Server</h1>");

});

const PORT = 3000;

server.listen(PORT, () => {

    console.log(
        `Server running at http://localhost:${PORT}`
    );

});
```

### Run

```bash
node server.js
```

Open:

```text
http://localhost:3000
```

### Viva

**Q. What is Node.js?**
A JavaScript runtime that allows JavaScript to run outside the browser.

**Q. What is the `http` module?**
A built-in Node.js module used to create HTTP servers and handle HTTP requests.

**Q. What does `createServer()` do?**
Creates an HTTP server.

**Q. What does `listen(3000)` do?**
Starts the server on port 3000.

---

# PRACTICAL 7 — Express Web Server with Multiple Routes

### Code

```javascript
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("<h1>Welcome to my website</h1>");
});

app.get("/about", (req, res) => {
    res.send("<h1>This is the About page</h1>");
});

app.get("/services", (req, res) => {
    res.send("<h1>This is the Services page</h1>");
});

app.get("/contact", (req, res) => {
    res.send(
        "<h1>Contact us at example@gmail.com</h1>"
    );
});

app.listen(3000, () => {
    console.log(
        "Server running on http://localhost:3000"
    );
});
```

### Run

```bash
npm init -y
npm install express
node app.js
```

### Viva

**Q. What is Express?**
A web framework for Node.js used to create servers, routes and APIs.

**Q. What is routing?**
Defining how the application responds to different URLs and HTTP methods.

**Q. What does `app.get()` do?**
Defines a route that responds to HTTP GET requests.

**Q. What are `req` and `res`?**
`req` is the request object and `res` is the response object.

---

# PRACTICAL 8 — REST API for Books

### Code

```javascript
const express = require("express");

const app = express();

app.use(express.json());

let books = [
    {
        id: 1,
        name: "The World of Death",
        author: "George Orwell"
    },
    {
        id: 2,
        name: "The Way of Death",
        author: "John Doe"
    },
    {
        id: 3,
        name: "The Theory of Death",
        author: "Someone"
    }
];


// GET all books

app.get("/books", (req, res) => {

    res.status(200).json({
        success: true,
        data: books,
        message: "Books fetched successfully"
    });

});


// GET book by ID

app.get("/books/:id", (req, res) => {

    const id = Number(req.params.id);

    const book = books.find(
        book => book.id === id
    );

    if (!book) {

        return res.status(404).json({
            success: false,
            message: "No Book Found"
        });

    }

    res.status(200).json({
        success: true,
        data: book,
        message: "Book fetched successfully"
    });

});


// POST - Add a new book

app.post("/books", (req, res) => {

    const newBook = {
        id: books.length + 1,
        ...req.body
    };

    books.push(newBook);

    res.status(201).json({
        success: true,
        data: newBook,
        message: "Book inserted successfully"
    });

});


// PUT - Update book

app.put("/books/:id", (req, res) => {

    const id = Number(req.params.id);

    const book = books.find(
        book => book.id === id
    );

    if (!book) {

        return res.status(404).json({
            success: false,
            message: "No Book Found"
        });

    }

    Object.assign(book, req.body);

    res.status(200).json({
        success: true,
        data: book,
        message: "Book updated successfully"
    });

});


// DELETE - Delete book

app.delete("/books/:id", (req, res) => {

    const id = Number(req.params.id);

    const index = books.findIndex(
        book => book.id === id
    );

    if (index === -1) {

        return res.status(404).json({
            success: false,
            message: "No Book Found"
        });

    }

    const deletedBook = books.splice(index, 1);

    res.status(200).json({
        success: true,
        data: deletedBook[0],
        message: "Book deleted successfully"
    });

});


app.listen(3000, () => {

    console.log(
        "Server running on http://localhost:3000"
    );

});
```

### Viva

**Q. What is REST API?**
An API that exposes resources through HTTP methods and URLs.

**Q. What does CRUD mean?**

```text
Create → POST
Read   → GET
Update → PUT
Delete → DELETE
```

**Q. What is `req.params.id`?**
The ID taken from a URL such as `/books/1`.

**Q. What is `req.body`?**
Data sent inside the request body.

**Q. Why `express.json()`?**
To parse JSON request bodies.

---

# PRACTICAL 9 — MongoDB User CRUD

### Code

```javascript
const express = require("express");
const mongoose = require("mongoose");

const app = express();

app.use(express.json());

const MONGO_URL =
    "mongodb://127.0.0.1:27017/usersdb";

mongoose.connect(MONGO_URL)
    .then(() => {
        console.log("Connected to MongoDB");
    })
    .catch(error => {
        console.log(error);
    });


const userSchema = new mongoose.Schema({
    name: String,
    email: String,
    age: Number
});

const User = mongoose.model("User", userSchema);


// Create user

app.post("/users", async (req, res) => {

    try {

        const user = await User.create(req.body);

        res.status(201).json({
            success: true,
            data: user,
            message: "User inserted successfully"
        });

    }
    catch(error) {

        res.status(500).json({
            success: false,
            message: error.message
        });

    }

});


// Read all users

app.get("/users", async (req, res) => {

    try {

        const users = await User.find();

        res.status(200).json({
            success: true,
            data: users,
            message: "Users fetched successfully"
        });

    }
    catch(error) {

        res.status(500).json({
            success: false,
            message: error.message
        });

    }

});


// Read one user

app.get("/users/:id", async (req, res) => {

    try {

        const user =
            await User.findById(req.params.id);

        if (!user) {

            return res.status(404).json({
                success: false,
                message: "User not found"
            });

        }

        res.status(200).json({
            success: true,
            data: user,
            message: "User fetched successfully"
        });

    }
    catch(error) {

        res.status(500).json({
            success: false,
            message: error.message
        });

    }

});


// Update user

app.put("/users/:id", async (req, res) => {

    try {

        const user =
            await User.findByIdAndUpdate(
                req.params.id,
                req.body,
                { new: true }
            );

        if (!user) {

            return res.status(404).json({
                success: false,
                message: "User not found"
            });

        }

        res.status(200).json({
            success: true,
            data: user,
            message: "User updated successfully"
        });

    }
    catch(error) {

        res.status(500).json({
            success: false,
            message: error.message
        });

    }

});


// Delete user

app.delete("/users/:id", async (req, res) => {

    try {

        const user =
            await User.findByIdAndDelete(
                req.params.id
            );

        if (!user) {

            return res.status(404).json({
                success: false,
                message: "User not found"
            });

        }

        res.status(200).json({
            success: true,
            message: "User deleted successfully"
        });

    }
    catch(error) {

        res.status(500).json({
            success: false,
            message: error.message
        });

    }

});


app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

### Viva

**Q. What is MongoDB?**
A NoSQL document-oriented database.

**Q. What is Mongoose?**
An ODM library used to work with MongoDB from Node.js.

**Q. What is a schema?**
It defines the structure and types of data.

**Q. What is a model?**
It provides methods to interact with a MongoDB collection.

**Q. What does `User.find()` do?**
Retrieves users.

**Q. What does `User.create()` do?**
Creates a new document.

---

# PRACTICAL 10 — Middleware / Centralized Request Logging

### Code

```javascript
const express = require("express");

const app = express();


// Custom middleware

const logger = (req, res, next) => {

    const log =
        `${new Date().toISOString()} - ` +
        `${req.method} ${req.url}`;

    console.log(log);

    next();
};

app.use(logger);


// Routes

app.get("/users/:id", (req, res) => {

    res.send(
        `User details for ID: ${req.params.id}`
    );

});

app.get("/product/:category/:id", (req, res) => {

    res.send(
        `Product category: ${req.params.category}, ` +
        `Product ID: ${req.params.id}`
    );

});

app.get("/error", (req, res) => {

    res.status(500).send(
        "Something broke on the server"
    );

});


app.listen(3000, () => {

    console.log(
        "Server is running on port 3000"
    );

});
```

### Viva

**Q. What is middleware?**
A function that runs between receiving a request and sending the response.

**Q. What are the parameters of middleware?**

```javascript
(req, res, next)
```

**Q. What does `next()` do?**
Passes control to the next middleware/route.

**Q. Why use logging middleware?**
To monitor requests and help with debugging.

---

# PRACTICAL 11 — Fetch API

### Code

```html
<!DOCTYPE html>
<html>

<head>
    <title>Fetch API Demo</title>
</head>

<body>

<h2>Fetch API Demo</h2>

<button onclick="loadUsers()">
    Load Users
</button>

<ul id="userList"></ul>

<script>

async function loadUsers() {

    try {

        const response = await fetch(
            "https://jsonplaceholder.typicode.com/users"
        );

        if (!response.ok) {
            throw new Error("Request failed");
        }

        const data = await response.json();

        const userList =
            document.getElementById("userList");

        data.forEach(user => {

            const li =
                document.createElement("li");

            li.textContent =
                `${user.name} - ${user.email}`;

            userList.appendChild(li);

        });

    }
    catch(error) {

        console.log("Error:", error);

        document.getElementById("userList")
            .innerHTML = "Error loading data";

    }

}

</script>

</body>
</html>
```

### Viva

**Q. What is Fetch API?**
It is used to make HTTP requests from JavaScript.

**Q. What does `fetch()` return?**
A Promise.

**Q. Why use `await response.json()`?**
To parse the response body as JSON.

**Q. What is `async`?**
It makes a function asynchronous and allows the use of `await`.

**Q. What is a Promise?**
It represents the eventual result of an asynchronous operation.

---

# PRACTICAL 12 — Real-Time Chat using Socket.IO

## Server

```javascript
const express = require("express");
const http = require("http");
const { Server } = require("socket.io");

const app = express();

const server = http.createServer(app);

const io = new Server(server);

app.get("/", (req, res) => {
    res.sendFile(__dirname + "/index.html");
});


io.on("connection", (socket) => {

    console.log("New user connected");

    socket.on("chat message", (msg) => {

        console.log("Message:", msg);

        io.emit("chat message", msg);

    });

    socket.on("disconnect", () => {

        console.log("User disconnected");

    });

});


server.listen(3000, () => {

    console.log(
        "Server running on http://localhost:3000"
    );

});
```

## Client — `index.html`

```html
<!DOCTYPE html>
<html>

<head>
    <title>Simple Chat</title>
</head>

<body>

<h2>Chat Application</h2>

<ul id="messages"></ul>

<input
    id="message"
    type="text"
    placeholder="Type a message"
>

<button onclick="sendMessage()">
    Send
</button>

<script src="/socket.io/socket.io.js"></script>

<script>

const socket = io();

function sendMessage() {

    const input =
        document.getElementById("message");

    const message = input.value;

    if (message.trim() === "") {
        return;
    }

    socket.emit("chat message", message);

    input.value = "";
}


socket.on("chat message", (msg) => {

    const li =
        document.createElement("li");

    li.textContent = msg;

    document
        .getElementById("messages")
        .appendChild(li);

});

</script>

</body>
</html>
```

### Viva

**Q. What is Socket.IO?**
A library for real-time, bidirectional communication between client and server.

**Q. What does `io.on("connection")` do?**
It handles a new client connection.

**Q. What does `socket.on()` do?**
Listens for an event.

**Q. What does `socket.emit()` do?**
Sends an event from a socket.

**Q. What does `io.emit()` do?**
Broadcasts an event to connected clients.

**Q. What is `disconnect`?**
It occurs when a client disconnects.

---

# PRACTICAL 13 — Unit Testing using Mocha

### Code

```javascript
const assert = require("assert");


// Function

function add(a, b) {
    return a + b;
}


// Hooks

before(function() {
    console.log("Before all tests");
});

beforeEach(function() {
    console.log("Before each test");
});

afterEach(function() {
    console.log("After each test");
});

after(function() {
    console.log("After all tests");
});


// Test cases

describe("Addition Function", function() {

    it("should return 5 when adding 2 and 3",
        function() {

            assert.strictEqual(
                add(2, 3),
                5
            );

        }
    );


    it("should increase by 1",
        function() {

            let count = 5;

            count = count + 1;

            assert.strictEqual(
                count,
                6
            );

        }
    );


    it("should increase by 2",
        function() {

            let count = 5;

            count = count + 2;

            assert.strictEqual(
                count,
                7
            );

        }
    );

});
```

### Run

```bash
npm install mocha
npx mocha
```

### Viva

**Q. What is Mocha?**
A JavaScript testing framework.

**Q. What is `describe()`?**
It groups related tests.

**Q. What is `it()`?**
It defines an individual test case.

**Q. What is `assert`?**
It verifies whether an actual result matches an expected result.

**Q. What is `before()`?**
Runs once before the tests.

**Q. What is `after()`?**
Runs once after the tests.

**Q. What is `beforeEach()`?**
Runs before every test.

**Q. What is `afterEach()`?**
Runs after every test.

---

# PRACTICAL 14 — Git Commands

### Code / Commands

```bash
# Initialize Git repository

git init


# Configure identity

git config --global user.name "Your Name"

git config --global user.email "your@email.com"


# Check status

git status


# Stage files

git add .


# Commit changes

git commit -m "First commit"


# Add remote repository

git remote add origin https://github.com/username/repository.git


# Push to GitHub

git push -u origin main
```

### Viva

**Q. What is Git?**
Git is a distributed version control system.

**Q. What is GitHub?**
A platform for hosting Git repositories and collaborating on code.

**Q. What does `git init` do?**
Initializes a Git repository.

**Q. What does `git add .` do?**
Stages the files for the next commit.

**Q. What does `git commit` do?**
Records a snapshot of staged changes in the **local repository**.

**Q. Does `git commit` upload files to GitHub?**

**NO.**

`git commit` → local repository.

`git push` → remote repository/GitHub.

**Q. What does `git status` do?**
Shows the current state of the working directory and staging area.

**Q. What does `git remote add origin` do?**
Connects the local repository to a remote repository.

**Q. What does `git push` do?**
Uploads local commits to the remote repository.

---

# 🔥 THE 25 VIVA QUESTIONS TO MEMORIZE FIRST

If you literally have **almost no time**, read ONLY this section.

```text
1. What is HTML?
→ HTML structures a webpage.

2. What is JavaScript?
→ JavaScript adds logic and interactivity.

3. What is DOM?
→ Document Object Model; JavaScript representation of HTML.

4. What does getElementById() do?
→ Selects an HTML element by ID.

5. What does .value do?
→ Gets the value of an input.

6. What does .innerHTML do?
→ Gets/changes HTML content.

7. What is Node.js?
→ JavaScript runtime outside the browser.

8. What is Express?
→ Web framework for Node.js.

9. What is a route?
→ Defines how a server responds to a URL/request.

10. What are req and res?
→ Request and response objects.

11. What is REST API?
→ API using resources and HTTP methods.

12. What is CRUD?
→ Create, Read, Update, Delete.

13. POST?
→ Create.

14. GET?
→ Read.

15. PUT?
→ Update.

16. DELETE?
→ Delete.

17. What is MongoDB?
→ NoSQL document database.

18. What is Mongoose?
→ ODM library for MongoDB and Node.js.

19. What is middleware?
→ Function that runs during request-response cycle.

20. What is next()?
→ Passes control to the next middleware/handler.

21. What is Fetch?
→ API for making HTTP requests.

22. What is Socket.IO?
→ Real-time bidirectional communication library.

23. What is Mocha?
→ JavaScript testing framework.

24. What is Git?
→ Distributed version control system.

25. Difference between commit and push?
→ Commit saves changes locally; push uploads commits to the remote.
```

---

## 🚨 And memorize this one chain

If examiner asks **"Explain how Git works"**, say:

> **"First `git init` initializes the repository. Then `git add` moves changes to the staging area. `git commit` records those staged changes in the local repository. Finally `git push` sends the commits to the remote repository such as GitHub."**

That's a **very safe viva answer**.

And if they ask **"Explain your Express CRUD API"**:

> **"I used Express to create routes. GET is used to read books, POST to create a book, PUT to update a book and DELETE to delete a book. `req.params` gets the ID from the URL and `req.body` gets the data sent by the client."**

**Your uploaded PDF contains these 14 practicals across pages 1–29; the organization above follows that sequence.** 

Now **copy this somewhere and go**. Don't spend the remaining time trying to understand every single line. **Know the skeleton + know what each important keyword means + be able to explain your program in 3–4 sentences.**
