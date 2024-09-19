<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1 class="text-uppercase">To Do List</h1>
      </div>

      <!-- form -->
      <div class="form">
        <input
          type="text"
          placeholder="New Task"
          v-model="newTask"
          @keyup.enter="emitAddTask"
        />
        <button @click="emitAddTask"><span class="mdi mdi-plus"></span></button>
      </div>

      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <todo-task-item
            v-bind:task="task"
            v-for="(task, index) in tasks"
            :key="task.id"
            @remove="emitRemoveTask(index)"
            @complete="emitCompleteTask(task)"
          ></todo-task-item>
        </ul>
      </div>

      <!-- buttons -->
      <div class="clearBtns">
        <button @click="emitClearCompleted">Clear completed</button>
        <button @click="emitClearAll">Clear all</button>
      </div>

      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ incomplete }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import TodoTaskItem from "./TodoTaskItem.vue";

export default {
  name: "TodoTask",
  props: ["tasks"],
  components: {
    TodoTaskItem,
  },
  data() {
    return {
      newTask: "",
    };
  },
  computed: {
    incomplete() {
      return this.tasks.filter((task) => !task.completed).length;
    },
  },
  methods: {
    emitAddTask() {
      if (this.newTask) {
        this.$emit("add-task", this.newTask);
        this.newTask = ""; // Reset the input field
      }
    },
    emitClearAll() {
      this.$emit("clear-all");
    },
    emitClearCompleted() {
      this.$emit("clear-completed");
    },
    emitCompleteTask(task) {
      this.$emit("complete-task", task);
    },
    emitRemoveTask(index) {
      this.$emit("remove-task", index);
    },
  },
};
</script>
