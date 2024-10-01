# exercise-build-an-api-to-manage-to-dos

## Learning Goals

Upon completing this exercise, you will be able to:

- Set up an Express.js server
- Implement CRUD operations in an Express.js API
- Manage data storage using an array
- Implement error handling for various scenarios

## Introduction

Welcome to the To Do API exercise! 📝

In this exercise, you will build a RESTful API to manage a list of to-dos. The API will allow users to create new to-dos, retrieve all to-dos, retrieve a specific to-do by ID, search for to-dos by various criteria, update a specific to-do by ID, and delete a to-do by ID.

Your task is to build this API using Express.js and ensure that it handles requests and responses correctly, including appropriate status codes and error handling.

To-dos should be stored in an array, with each To-do represented as an object with the following keys:

- `id`
- `name`
- `description`
- `status`

Here’s an example of a sample to-do:

```jsx
{
  "id": 1,
  "name": "Buy groceries",
  "description": "Milk, Bread, Cheese, Eggs",
  "status": "Open" // other statuses could be "In Progress" and "Done"
}

```

## Getting Started

1. [Fork this repository](https://github.com/code-verge/exercise-valentinos-express-site/)
2. Clone the repository to your computer
3. Open the repository in VS Code
4. Follow instructions

## **Instructions**

Welcome to the To-do API project! This is where all of your knowledge about Express.js and designing RESTful web services comes together…

Let’s build a powerful API to manage your to-dos! 🚀

### Task 1

After forking and cloning the repository, you will find an empty Node.js project. We have already initialized it, so you should see an existing `package.json` file.

Your first task is to **install Express** and **create** an `app.js` **file.** 
Your project structure should look like the following:

```html
todo-api/
│
├── app.js
├── package.json
```

### Task 2

Open `app.js` and set up an Express Server to listen to incoming HTTP requests.

<aside>
ℹ️

Remember, you can use port 3000.

If you receive an error that the port is already in use, then it means that you have an existing instance of an Express Server already running on the same port.

You need to locate it and terminate the Express Server first.

</aside>

### Task 3

Create an `array` to store your to-dos. Each to-do should be an `object` with the following keys:

- `id`
- `name`
- `description`
- `status`

### Task 4

Implement the endpoint `/todos` to create a new to-do (`POST`).

When this endpoint is called with valid data, it should return the newly created to-do object with a unique `id`.

Ensure that the request body contains all the required fields 
(`name`, `description`, and `status`). 

If any field is missing, respond with a `400 Bad Request` status and an appropriate error message.

Check the FAQ section at the end of this exercise for another way to generate unique IDs, which is more reliable than checking the length of the array and incrementing by 1.

### Task 5

Implement the endpoint `/todos` to retrieve all to-dos (`GET`).

The response should contain an array of all to-do objects.

### Task 6

Implement the endpoint to retrieve a specific to-do by its ID.

Follow RESTful best practices and common naming conventions when designing this endpoint. If a to-do with the specified ID is found, return it with a `200 status` code. If not found, respond with a `404 status` and an appropriate error message.

### Task 7

Implement the endpoint to search for to-dos by `name` and `status` .

Use query parameters to specify the search criteria. 

If no matching to-dos are found, return an empty array. If invalid search criteria are provided, respond with a `400 Bad Request` status and an appropriate error message.

### Task 8

Implement the endpoint to update a specific to-do by its ID (`PUT`).

Respond with the updated to-do object.

If the to-do with the specified `id` is not found, respond with a `404 Not Found` status and an appropriate error message.

### Task 9

Implement the endpoint to delete a specific to-do by its ID.

If the to-do with the specified `id` is not found, respond with a `404 Not Found` status and an appropriate error message. If the `id` is found and the deletion is successful, respond with an appropriate success message, e.g. `To-do was deleted successfully` .

### Task 10

Test your endpoints withe the Bruno API client. Create a new collection in Bruno and validate that your API works as expected!

## **Submission**

When you've completed the exercise:

1. Run the following commands:

```jsx
git add .
git commit -m "Completed To-do API"
git push origin main
```

1. Create a Pull Request and submit your assignment.

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
