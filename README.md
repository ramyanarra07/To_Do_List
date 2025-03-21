# Ex03 To-Do List using JavaScript
## Date:21-03-2025

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
DEVELOPED BY :NARRA RAMYA

REG NO :212223040128

```
**##HTML**

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Todo List</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Todo App</h1>
    <div class="todo-container">
        <input type="text" id="todo-input" placeholder="Add new todo">
        <button id="add-todo-btn">Add</button>
    </div>
    
    <ul id="todo-list"></ul>
    <div class="clear-completed-container">
        <button id="clear-completed-btn">Clear All</button>
    </div>
    

    <script src="script.js"></script>
</body>
</html>

**##CSS**

body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
    background-image: url('todobg.jpg');
    background-size: cover;
    background-position: center;

}

.container {
    width: 50%;
    margin: 40px auto;
    padding: 20px;
    background-color: #fff;
    border: 1px solid #ddd;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    text-align: center;
    border-radius: 10px;
}

h1 {
    margin-bottom: 20px;
    color: #333;
    text-align: center;
}
.todo-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
    position: relative;
}

#todo-input {
    width: 30%;
    height: 30px;
    padding: 10px;
    font-size: 18px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

#add-todo-btn {
    width: 10%;
    height: 40px;
    padding: 10px;
    font-size: 18px;
    background-color: lightcoral;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-left: 10px;
}



#todo-list {
    list-style: none;
    padding: 0;
    margin: 20px auto; 
    width: 50%; 
    display: flex;
    flex-direction: column;
    align-items: center; 
}

.todo-item {
    width: 100%; 
    padding: 10px;
    border-bottom: 1px solid #ccc;
    display: flex;
    justify-content: space-between; 
    align-items: center;
    background: white;
    border-radius: 5px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}


.todo-item:last-child {
    border-bottom: none;
}

.completed {
    text-decoration: line-through;
    color: #666;
}

#filter-container {
    margin-top: 20px;
    display: flex;
    justify-content: space-evenly;
    align-items: center;
}

#filter-container button {
    width: 10%;
    height: 40px;
    padding: 10px;
    font-size: 18px;
    background-color:lightcoral;
    color: #fff;
    border: none;
    border-radius: 2px;
    cursor: pointer;
    justify-content: center;
}

#filter-container button:hover {
    background-color: #ccc;
}
.clear-completed-container {
    display: flex;
    justify-content: center; 
    align-items: center; 
    margin-top: 20px; 
}

#clear-completed-btn {
    background-color: lightcoral;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    padding: 10px 20px;
    font-size: 16px;
    display: inline-block; 
    text-align: center;
}

#clear-completed-btn:hover {
    background-color:lightcoral;
}
**##JS**

// Get elements
const todoInput = document.getElementById('todo-input');
const addTodoBtn = document.getElementById('add-todo-btn');
const todoList = document.getElementById('todo-list');
const allTodosBtn = document.getElementById('all-todos-btn');
const activeTodosBtn = document.getElementById('active-todos-btn');
const completedTodosBtn = document.getElementById('completed-todos-btn');
const clearCompletedBtn = document.getElementById('clear-completed-btn');

// Initialize todos array
let todos = [];

// Load todos from local storage
if (localStorage.getItem('todos')) {
    todos = JSON.parse(localStorage.getItem('todos'));
}

// Function to render todos
function renderTodos() {
    todoList.innerHTML = '';
    todos.forEach((todo, index) => {
        const todoElement = document.createElement('li');
        todoElement.textContent = todo.text;
        if (todo.completed) {
            todoElement.classList.add('completed');
        }
        todoElement.addEventListener('click', () => {
            toggleCompleted(index);
        });
        const deleteBtn = document.createElement('button');
        deleteBtn.textContent = 'Delete';
        deleteBtn.addEventListener('click', () => {
            deleteTodo(index);
        });
        todoElement.appendChild(deleteBtn);
        todoList.appendChild(todoElement);
    });
}

// Function to add todo
function addTodo() {
    const todoText = todoInput.value.trim();
    if (todoText) {
        todos.push({ text: todoText, completed: false });
        todoInput.value = '';
        renderTodos();
        saveTodosToLocalStorage();
    }
}

// Function to delete todo
function deleteTodo(index) {
    todos.splice(index, 1);
    renderTodos();
    saveTodosToLocalStorage();
}

// Function to toggle completed
function toggleCompleted(index) {
    todos[index].completed = !todos[index].completed;
    renderTodos();
    saveTodosToLocalStorage();
}

// Function to save todos to local storage
function saveTodosToLocalStorage() {
    localStorage.setItem('todos', JSON.stringify(todos));
}

// Function to clear completed todos
function clearCompletedTodos() {
    todos = todos.filter(todo => !todo.completed);
    renderTodos();
    saveTodosToLocalStorage();
}

// Event listeners
addTodoBtn.addEventListener('click', addTodo);
allTodosBtn.addEventListener('click', () => {
    renderTodos();
});
activeTodosBtn.addEventListener('click', () => {
    const activeTodos = todos.filter(todo => !todo.completed);
    todoList.innerHTML = '';
    activeTodos.forEach((todo, index) => {
        const todoElement = document.createElement('li');
        todoElement.textContent = todo.text;
        todoList.appendChild(todoElement);
    });
});
completedTodosBtn.addEventListener('click', () => {
    const completedTodos = todos.filter(todo => todo.completed);
    todoList.innerHTML = '';
    completedTodos.forEach((todo, index) => {
        const todoElement = document.createElement('li');
        todoElement.textContent = todo.text;
        todoElement.classList.add('completed');
        todoList.appendChild(todoElement);
    });
});
clearCompletedBtn.addEventListener('click', clearCompletedTodos);


```


## OUTPUT:
![image](https://github.com/user-attachments/assets/cd548d3c-c7e5-4548-a861-71dd322cc528)

![image](https://github.com/user-attachments/assets/6b7916e5-4e9b-44f9-aabf-d6da903f6dd8)



## RESULT
The program for creating To-do list using JavaScript is executed successfully.
