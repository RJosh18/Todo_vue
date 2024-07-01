<template>
  <div class="p-3">
    <div
      v-for="todo in todos"
      :key="todo.id"
      class="flex items-center justify-between mb-2"
    >
      <div class="flex items-center" @click="toggleCompletion(todo)">
        <label
          :class="{ 'line-through': todo.completed }"
          class="cursor-pointer font-semibold"
          >{{ todo.item }}</label
        >
        <p class="text-gray-500 text-sm ml-2">{{ todo.time }}</p>
      </div>
      <div class="flex items-center">
        <button @click="removeHandler(todo.id)" class="text-red-500">
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoBox",
  props: {
    todos: {
      type: Array,
      required: true,
    },
    removeHandler: {
      type: Function,
      required: true,
    },
    toggleCompletionHandler: {
      type: Function,
      required: true,
    },
  },
  methods: {
    toggleCompletion(todo) {
      this.toggleCompletionHandler(todo);
    },
  },
};
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
  color: #ccc;
  cursor: pointer;
}
</style>
