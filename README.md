# -Checkpoint-Managing-State-in-React

Here's a simple implementation of a To-Do List application using React that meets the requirements you've specified. This application includes components for adding, editing, deleting tasks, and marking them as completed, along with form validation and browser storage for persistence.

File Structure```
/todo-app│├── /src│ ├── /components│ │ ├── TaskForm.js│ │ ├── TaskItem.js│ │ └── TaskList.js│ ├── App.js│ ├── index.js│ └── styles.css│└── README.md```

Code Implementation####1. App.js```jsximport React, { useEffect, useState } from 'react';
import TaskList from './components/TaskList';
import TaskForm from './components/TaskForm';
import './styles.css';

const App = () => {
const [tasks, setTasks] = useState([]);
// Load tasks from localStorage when the app initializes useEffect(() => {
const loadedTasks = JSON.parse(localStorage.getItem('tasks')) || [];
setTasks(loadedTasks);
}, []);

// Save tasks to localStorage whenever tasks change useEffect(() => {
localStorage.setItem('tasks', JSON.stringify(tasks));
}, [tasks]);

return (

<div className="App"> <h1>To-Do List</h1> <TaskForm setTasks={setTasks} /> <TaskList tasks={tasks} setTasks={setTasks} /> </div> ); };
export default App;

ini

####2. components/TaskForm.js```jsximport React, { useState } from 'react';  

const TaskForm = ({ setTasks }) => {  
 const [name, setName] = useState('');  
 const [description, setDescription] = useState('');  

 const handleSubmit = (e) => {  
 e.preventDefault();  
 if (!name || !description) {  
 alert('Please fill out both fields');  
 return;  
 }  
 const newTask = {  
 id: Date.now(),  
 name,  
 description,  
 completed: false,  
 };  
 setTasks(prevTasks => [...prevTasks, newTask]);  
 setName('');  
 setDescription('');  
 };  

 return (  
 <form onSubmit={handleSubmit}>  
 <input type="text"  
 placeholder="Task Name"  
 value={name}  
 onChange={(e) => setName(e.target.value)}  
 required />  
 <input type="text"  
 placeholder="Task Description"  
 value={description}  
 onChange={(e) => setDescription(e.target.value)}  
 required />  
 <button type="submit">Add Task</button>  
 </form>  
 );  
};  

export default TaskForm;  
####3. components/TaskList.js```jsximport React from 'react';
import TaskItem from './TaskItem';

const TaskList = ({ tasks, setTasks }) => {
const updateTask = (id, updatedTask) => {
setTasks(tasks.map(task => (task.id === id ? updatedTask : task)));
};

const deleteTask = (id) => {
if (window.confirm('Are you sure you want to delete this task?')) {
setTasks(tasks.filter(task => task.id !== id));
}
};

return (

<ul> {tasks.map(task => ( <TaskItem key={task.id} task={task} updateTask={updateTask} deleteTask={deleteTask} /> ))} </ul> ); };
export default TaskList;

ini

####4. components/TaskItem.js```jsximport React, { useState } from 'react';  

const TaskItem = ({ task, updateTask, deleteTask }) => {  
 const [isEditing, setIsEditing] = useState(false);  
 const [formData, setFormData] = useState(task);  

 const handleEdit = () => {  
 setIsEditing(!isEditing);  
 };  

 const handleUpdate = (e) => {  
 e.preventDefault();  
 updateTask(task.id, formData);  
 setIsEditing(false);  
 };  

 const handleChange = (e) => {  
 const { name, value } = e.target;  
 setFormData({ ...formData, [name]: value });  
 };  

 const toggleCompletion = () => {  
 updateTask(task.id, { ...task, completed: !task.completed });  
 };  

 return (  
 <li className={task.completed ? 'completed' : ''}>  
 {isEditing ? (  
 <form onSubmit={handleUpdate}>  
 <input type="text"  
 name="name"  
 value={formData.name}  
 onChange={handleChange}  
 />  
 <input type="text"  
 name="description"  
 value={formData.description}  
 onChange={handleChange}  
 />  
 <button type="submit">Update</button>  
 </form>  
 ) : (  
 <>  
 <span onClick={toggleCompletion} style={{ cursor: 'pointer' }}>  
 {task.name}  
 </span>  
 <button onClick={handleEdit}>Edit</button>  
 <button onClick={() => deleteTask(task.id)}>Delete</button>  
 </>  
 )}  
 </li>  
 );  
};  

export default TaskItem;  
####5. styles.css```css.App {
max-width:600px;
margin: auto;
text-align: center;
}

form {
margin:20px0;
}

input {
margin:010px;
padding:8px;
}

button {
padding:8px12px;
margin:05px;
}

li {
list-style: none;
display: flex;
justify-content: space-between;
margin:10px0;
}

.completed {
text-decoration: line-through;
color: gray;
}

graphql

### README.md```markdown# To-Do List ApplicationA simple To-Do List application built with React that allows users to add, edit, delete, and mark tasks as completed. This application uses browser local storage for persisting tasks between sessions.  

## Features- Add new tasks with a name and description- Edit existing tasks- Delete tasks with confirmation- Mark tasks as completed- Form validation ensures both fields are filled- Persist tasks using localStorage## Technologies Used- React- CSS for styling## Getting Started1. Clone the repository:  
git clone https://github.com/yourusername/todo-app.git ```
2. Navigate to the project directory:

bash
cd todo-app ```  
3. Install dependencies:  
npm install ```
4. Start the application:

php
npm start ```  
5. Open your browser and go to `http://localhost:3000` to view the application.  

## ContributionsFeel free to submit issues or pull requests for any improvements or suggestions.  
ConclusionThis implementation covers the requirements outlined in your project description. You can customize the styles and expand the functionality as desired, such as adding priority or due dates. Make sure to test the application thoroughly to ensure all functionalities work as expected.
