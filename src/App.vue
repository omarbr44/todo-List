<script >
export default{
  data() {
    return{
      newTask: "",
      tasks: [
        { title: "example", completed: false, id: 1 },
      ],
      filter: "all",
      ids: 3
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== "") {
        this.tasks.push({ title: this.newTask, completed: false, id: ++this.ids });
        this.newTask = "";
      }
    },
    deleteTask(id) {
     this.tasks = this.tasks.filter((t)=> t.id != id)
    },
    filterTasks(filter) {
      this.filter = filter;
    },
  },
  computed: {
    filteredTasks() {
      if (this.filter === "all") {
        return this.tasks;
      } else if (this.filter == "active") {
        return this.tasks.filter((task) => !task.completed);
      } else if (this.filter == "completed") {
        return this.tasks.filter((task) => task.completed);
      }
    },
  },
}

  

</script>

<template>
    <div id="app">
      <h1>Todo List</h1>
      <form @submit.prevent="addTask">
        <input type="text" v-model="newTask" placeholder="Add a new task" />
        <button type="submit">Add</button>
      </form>
      <ul>
        <li v-for="(task, index) in filteredTasks" :key="index">
          <input type="checkbox" v-model="task.completed" />
          <span :class="{ completed: task.completed }">{{ task.title }}</span>
          <button @click="deleteTask(task.id)">Delete</button>
        </li>
      </ul>
      <div>
        <button @click="filterTasks('all')">All</button>
        <button @click="filterTasks('active')">Active</button>
        <button @click="filterTasks('completed')">Completed</button>
      </div>
    </div>
</template>

<style scoped>
/* Reset default margins and paddings */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Set a base font size and family */
body {
  font-size: 16px;
  font-family: Arial, sans-serif;
}

/* Styling for the app container */
#app {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}

/* Styling for the heading */
h1 {
  font-size: 24px;
  margin-bottom: 20px;
}

/* Styling for the form */
form {
  display: flex;
  margin-bottom: 20px;
}

/* Styling for the input text box */
input[type="text"] {
  flex-grow: 1;
  padding: 10px;
  font-size: 16px;
  border: none;
  border-radius: 4px;
}

/* Styling for the add button */
button[type="submit"] {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button[type="submit"]:hover {
  background-color: #45a049;
}

/* Styling for the to-do list */
ul {
  list-style-type: none;
  margin-bottom: 20px;
}

/* Styling for the to-do list item */
li {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

/* Styling for the checkbox */
input[type="checkbox"] {
  margin-right: 10px;
}

/* Styling for completed tasks */
span.completed {
  text-decoration: line-through;
  color: #888;
}

/* Styling for the delete button */
button {
  padding: 5px 10px;
  font-size: 14px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-left: 1rem;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #d32f2f;
}

/* Styling for the filter buttons */
div button {
  margin-right: 10px;
  padding: 5px 10px;
  font-size: 14px;
  background-color: #e0e0e0;
  color: black;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

div button.active {
  background-color: #ccc;
}

/* Animation for fade-in effect */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Apply fade-in animation to list items */
li {
  animation: fadeIn 0.5s ease;
}
</style>
