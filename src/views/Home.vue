<template>
  <AddTask v-show="showAddTask" @add-new-task="addNewTask" />
  <Tasks
    @toggle-task-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
  name: "Home",
  props: {
    showAddTask: Boolean,
  },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async deleteTask(id) {
      if (confirm("Are you sure , you want to delete? ")) {
        const res = await fetch(`http://localhost:5000/tasks/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error Deleting task");
      }
    },
    async toggleReminder(id) {
      // console.log(id);
      const tasks = await this.fetchTasks();
      for (let i = 0; i < tasks.length; i++) {
        if (id == tasks[i].id) {
          tasks[i].reminder = !tasks[i].reminder;
          const res = await fetch(`http://localhost:5000/tasks/${id}`, {
            method: "PUT",
            headers: {
              "Content-type": "application/json",
            },
            body: JSON.stringify(tasks[i]),
          });
          this.tasks = await this.fetchTasks();
          // return res.json();
        }
      }
    },
    async addNewTask(data) {
      const res = await fetch("http://localhost:5000/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(data),
      });
      const task = await res.json();
      // console.log(data);
      this.tasks.push(task);
    },
    async fetchTasks() {
      const res = await fetch("http://localhost:5000/tasks");

      const data = await res.json();
      // console.log(data)
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`http://localhost:5000/tasks/${id}`);

      const data = await res.json();

      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>