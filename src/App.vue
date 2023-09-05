<template>
  <!-- App container -->
  <div class="container">
    <!-- Header component with event listener and props -->
    <Header @toggle-add-task="onToggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <!-- AddTask component conditionally rendered based on showAddTask -->
    <div v-show="showAddTask">
      <!-- AddTask component with event listener -->
      <AddTask @add-task="addTask" />
    </div>
    <!-- Tasks component with event listeners and props -->
    <Tasks
      @toggle-reminder="onToggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
// Import Vue components
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      // Data for tasks and UI state
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    // Toggle the display of the AddTask component
    onToggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    // Add a new task to the tasks array
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    // Delete a task by its ID
    deleteTask(id) {
      if (confirm("Are you Sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    // Toggle the reminder property of a task by its ID
    onToggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },
  created() {
    // Initialize tasks with sample data
    this.tasks = [
      {
        id: 1,
        text: "Pre demo",
        day: "1st Oct 2023",
        reminder: true,
      },
      {
        id: 2,
        text: "Pre demo",
        day: "1st Oct 2023",
        reminder: true,
      },
      {
        id: 3,
        text: "Pre demo",
        day: "1st Oct 2023",
        reminder: true,
      },
    ];
  },
};
</script>

<style>


@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Poppins", sans-serif;
}

.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
