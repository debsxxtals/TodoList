<template>
  <v-app id="inspire"> 
    <v-navigation-drawer v-model="drawer" app expand-on-hover rail>
      <!--  -->
      <v-list>
        <v-list-item
          prepend-avatar="https://randomuser.me/api/portraits/women/85.jpg"
          subtitle="sandra_a88@gmailcom"
          title="Sandra Adams"
        ></v-list-item>
      </v-list>

      <v-divider></v-divider>

      <v-list density="compact" nav>
        <v-list-item
          prepend-icon="mdi-folder"
          title="My Files"
          value="myfiles"
        ></v-list-item>
        <v-list-item
          prepend-icon="mdi-account-multiple"
          title="Shared with me"
          value="shared"
        ></v-list-item>
        <v-list-item
          prepend-icon="mdi-star"
          title="Starred"
          value="starred"
        ></v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Application</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <!--  -->
      <div id="app">
        <todo-task
          v-bind:tasks="tasks"
          @add-task="addTask"
          @clear-all="clearAllTasks"
          @clear-completed="clearCompletedTasks"
          @remove-task="removeTask"
          @complete-task="completeTask"
        ></todo-task>
      </div>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref } from "vue";

const drawer = ref(null);
</script>

<script>
import TodoTask from "./components/TodoTask.vue"; // Updated import

export default {
  name: "App",
  components: {
    TodoTask, // Use the updated component name
  },
  data() {
    return {
      tasks: [
        { id: 1, title: "Learn Vue JS", completed: true },
        { id: 2, title: "Watch Netflix", completed: true },
        { id: 3, title: "Go shopping", completed: false },
        { id: 4, title: "Learn guitar", completed: false },
        { id: 5, title: "Send email", completed: false },
      ],
    };
  },
  methods: {
    addTask(taskTitle) {
      this.tasks.push({ title: taskTitle, completed: false });
    },
    clearAllTasks() {
      this.tasks = [];
    },
    clearCompletedTasks() {
      this.tasks = this.tasks.filter((task) => !task.completed);
    },
    completeTask(task) {
      task.completed = !task.completed;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>
