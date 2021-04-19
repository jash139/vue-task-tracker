<template>
  <div class="container">
    <Header title="Task Tracker" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    toggleReminder(id) {
      const taskIndex = this.tasks.findIndex((task) => task.id == id);
      this.tasks[taskIndex].reminder = !this.tasks[taskIndex].reminder;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    addTask(task) {
      const newTask = {
        ...task,
        id: this.tasks.length + 1,
      };
      this.tasks.push(newTask);
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Appointment",
        day: "1st March",
        reminder: true,
      },
      {
        id: 2,
        text: "Meeting",
        day: "21st March",
        reminder: true,
      },
      {
        id: 3,
        text: "Dancing",
        day: "32nd December",
        reminder: false,
      },
      {
        id: 4,
        text: "Something",
        day: "2nd Feb",
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
