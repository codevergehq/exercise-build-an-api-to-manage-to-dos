# exercise-build-an-api-to-manage-to-dos

## Learning Goals

Upon completing this exercise, you will be able to:

- Set up an Express.js server
- Implement CRUD operations in an Express.js API
- Manage data storage using an array
- Implement RESTful API design principles
- Handle query parameters for searching

## Introduction

Welcome to the To Do API exercise! 📝

In this exercise, you will build a RESTful API to manage a list of to-dos. The API will follow strict REST conventions and allow users to create, read, update, and delete to-dos, as well as search for them using query parameters.

Please disregard the previous to-do list app from Project 1. This API design will follow specific conventions that are essential to follow, as we'll be building upon this later with React.

To-dos will be stored in an array, with each To-do represented as an object.

Here is a sample showing the to-do object structure:

```jsx
{
  "id": "uuid-here",
  "name": "Buy groceries",
  "done": false,
  "category": "shopping"
}

```

## Getting Started

1. Fork this repository
2. Clone the repository to your computer
3. Open the repository in VS Code
4. Follow instructions

## **Instructions**

Let's go ahead and build a RESTful API to manage your to-dos! 🚀

### Task 1

After forking and cloning the repository, you will find an empty project with nothing more than a `.gitignore` file and a `readme.md` file.

Let’s set this up and initialize this as a new Node.js project.

Your project structure should look like the following:

After you’ve cloned the repository locally, enter the project directory:


```bash
# Enter project directory
cd exercise-build-an-api-to-manage-to-dos
```

Now let’s initialize this as a Node.js project by running the following command in your terminal:

```bash
npm init -y
```

This will create a `package.json` file with default values.

Now install the required dependencies:

- Express.js
- UUID

```bash
# Install Express.js
npm install express

# Install UUID package
npm install uuid
```

> [!NOTE]  
> The UUID package generates unique identifiers (UUIDs) that we can use to ensure each to-do has a unique ID. This is more reliable than using incrementing numbers since UUIDs have an extremely low probability of collision, even across different systems.




Finally, create an `app.js` file in the project root directory.
Your project structure should now look as follows:

```bash
exercise-build-an-api-to-manage-to-dos/
│
├── node_modules/
├── .gitignore
├── app.js
├── package-lock.json
├── package.json
└── README.md

```

> [!NOTE]
> Although node_modules is visible in our project working directory, it should not be committed to version control. The node_modules directory contains all the installed dependencies and can be quite large. It will be automatically generated when someone runs npm install, so we don't need to track it in our repository. Our `.gitignore` file already contains the necessary configuration to ignore the node_modules directory, along with other common files and directories that shouldn't be tracked in version control.

### Task 2

Open ⁠`app.js` and set up an Express Server to listen to incoming HTTP requests:


```jsx
const express = require('express');
const { v4: uuidv4 } = require('uuid');

const app = express();

// Middleware to parse JSON bodies
app.use(express.json());

const port = 3000;

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```



> [!NOTE]
> Remember, you can use port 3000. If you receive an error that the port is already in use, then it means that you have an existing instance of an Express Server already running on the same port. You need to locate it and terminate the Express Server first.


### Task 3

In `app.js`, create an `array` to store your to-dos.

```jsx
// Array to store todos
const todos = [];
```

Each to-do in this array must strictly follow this structure:
	•	⁠`id` : string (UUID format)
	•	⁠`name` : string
	•	⁠`done` : boolean
	•	⁠`category` : string

### Task 4

Implement the endpoint to create a new to-do on the route ⁠`/todos` using the ⁠`POST` method.

When this endpoint is called with valid data, it should return the newly created to-do object with a unique `id`.

This endpoint will accept a JSON payload containing the required fields for a new to-do item and return the created to-do with its assigned UUID.
When this endpoint is called with valid data, it should return the newly created to-do object with a unique ⁠`id`.

> [!NOTE]
> Make sure to check out the FAQ section at the end of this exercise to see how you can generate unique IDs using the UUID library, which is more reliable than checking the length of the array and incrementing by 1.

Ensure that the request body contains all the required fields (⁠`name`, ⁠`done`, and ⁠`category`).

The ⁠`id` should be auto-generated using the UUID library. In the request body, you can set ⁠`done = false` as the default value of any newly created to-do.

When a `POST` request is made to create a new to-do, the server should automatically assign a UUID to ensure each to-do has a globally unique identifier.
If any field is missing, respond with a ⁠`400 Bad Request` status and an appropriate error message.

### Task 5

Implement the endpoint to get all to-dos on the route `⁠/todos` using the ⁠`GET` method.

The response should contain an array of all to-do objects in your ⁠`todos` array.

### Task 6

Implement search functionality on the ⁠`/todos` endpoint using query parameters:

	•	⁠`name` : Filter to-dos by name (case-insensitive partial match)
	•	⁠`done` : Filter to-dos by completion status (true/false)
	•	⁠`category` : Filter to-dos by category (exact match)

Example queries:

`GET /todos?done=false`
`GET /todos?name=grocery`
`GET /todos?category=shopping`

### Task 7

Implement the endpoint to get a specific to-do by ID using the route `⁠/todos/:id` with the ⁠`GET` method.

### Task 8

Implement the endpoint to update a specific to-do using the route ⁠`/todos/:id` with the ⁠`PUT` method.

### Task 9

Implement the endpoint to delete a specific to-do using the route ⁠`/todos/:id` with the ⁠`DELETE` method.

### Task 10

Test your API using Bruno.

Create a new collection with the following requests:

1. Get all todos — ⁠`GET http://localhost:3000/todos`
2. Search todos


``` jsx
GET http://localhost:3000/todos?done=false
GET http://localhost:3000/todos?category=shopping
GET http://localhost:3000/todos?name=groceries`
```


3. Create todo


``` jsx
POST http://localhost:3000/todos
Content-Type: application/json

{
  "name": "Buy groceries",
  "category": "shopping",
  "done": false
}
```


4. Get todo by ID — ⁠`GET http://localhost:3000/todos/:id`

5. Update todo


``` jsx
PUT http://localhost:3000/todos/:id
Content-Type: application/json

{
  "name": "Buy groceries",
  "category": "shopping",
  "done": true
}
```


6. 	Delete todo — ⁠`DELETE http://localhost:3000/todos/:id`



## **Submission**

When you've completed the exercise:

Run the following commands:

```jsx
git add .
git commit -m "Completed Todo API"
git push origin main
```

Create a Pull Request and submit your assignment.

Happy coding! 🙂

## Frequently Asked Questions (FAQs)

<details>
<summary>How do I handle errors in Express.js?</summary>

You can handle errors in Express.js using the `res.status(code).send("message")` method. 
    
    For example:
    
    ```jsx
    const todoId = parseInt(req.params.id, 10);
    const todo = todos.find((t) => t.id === todoId);
    
    if (!todo) {
      return res.status(404).send("To Do not found");
    }
    ```

</details>
    


<details>
<summary>How do I generate unique IDs for my to-dos?</summary>

As we’re working with a local array to store our collections of to-dos, we could simply check the length of the array and increment the ID by 1 (`array.length +1` ).
    
    This works but it’s not a foolproof solution. If we create to-dos, delete existing ones, and then create additional to-dos, we may end up introducing items with duplicate IDs (using the logic above).
    
    Another way to ensure that we generate unique IDs for the to-do objects is to use a third-party library such as `uuid` 
    
    To use this library, you can do the following:
    
    1. Install the `uuid` library with `npm install uuid` 
    2. Require the library in your code using `const { v4: uuidv4 } = require('uuid');`
    3. Use the `uuidv4()` method to generate unique IDs for your to-dos. This method ensures uniqueness in your IDs so there’s no need to check for existing IDs
    
    ```jsx
    const newTodo = {
        id: uuidv4(), // Generate a unique ID
        name,
        description,
        status
      };
    ```
</details>
