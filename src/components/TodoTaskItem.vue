<template>
  <li>
    <label>
      <input
        type="checkbox"
        :checked="task.completed"
        @change="toggleComplete"
      />
      {{ task.title }}
    </label>
    <button @click="$emit('remove')">
      <span class="mdi mdi-trash-can"></span>
    </button>
  </li>
</template>

<script>
export default {
  name: "TodoTaskItem",
  props: ["task"],
  methods: {
    toggleComplete(event) {
      this.$emit("complete", { ...this.task, completed: event.target.checked });
    },
  },
};
</script>

<style scoped>
/* Add your styles here */
</style>
