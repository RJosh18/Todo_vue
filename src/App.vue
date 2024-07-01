<template>
  <div id="app" class="container mx-auto mt-6">
    <div class="max-w-lg mx-auto">
      <div class="bg-white shadow-md rounded-lg p-6">
        <header class="text-center text-2xl font-bold mb-4">Todo List</header>

        <div class="mb-4 flex items-center">
          <input
            v-model="newTodo"
            type="text"
            placeholder="Enter a new todo..."
            class="w-64 px-3 py-2 border border-gray-300 rounded-md mr-2"
          />
          <button
            @click="addTodo"
            class="px-4 py-2 bg-blue-500 text-white rounded-md"
          >
            Add Todo
          </button>
        </div>

        <div class="mb-4">
          <button
            @click="filter = 'all'"
            :class="{
              'bg-blue-500 text-white': filter === 'all',
              'bg-gray-300': filter !== 'all',
            }"
            class="px-4 py-2 mr-2 rounded-md"
          >
            All
          </button>
          <button
            @click="filter = 'active'"
            :class="{
              'bg-blue-500 text-white': filter === 'active',
              'bg-gray-300': filter !== 'active',
            }"
            class="px-4 py-2 mr-2 rounded-md"
          >
            Active
          </button>
          <button
            @click="filter = 'completed'"
            :class="{
              'bg-blue-500 text-white': filter === 'completed',
              'bg-gray-300': filter !== 'completed',
            }"
            class="px-4 py-2 mr-2 rounded-md"
          >
            Completed
          </button>
        </div>

        <div>
          <TodoBox
            :todos="filteredTodos"
            :removeHandler="removeTodo"
            :toggleCompletionHandler="toggleCompletion"
          />
        </div>

        <div class="mt-4 text-center">
          Total Tasks: {{ todos.length }}<br />
          Tasks Left: {{ todos.filter((todo) => !todo.completed).length }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, computed } from "vue";
import TodoBox from "./components/TodoBox.vue";

export default {
  name: "App",
  components: {
    TodoBox,
  },
  setup() {
    const todos = ref([
      // { id: 1, item: "Task 1", completed: false, time: "10:00 AM" },
      // { id: 2, item: "Task 2", completed: false, time: "11:00 AM" },
      // { id: 3, item: "Task 3", completed: true, time: "12:00 PM" },
    ]);
    const newTodo = ref("");
    const filter = ref("all");

    const filteredTodos = computed(() => {
      if (filter.value === "all") {
        return todos.value;
      } else if (filter.value === "active") {
        return todos.value.filter((todo) => !todo.completed);
      } else if (filter.value === "completed") {
        return todos.value.filter((todo) => todo.completed);
      }
      return todos.value;
    });

    function addTodo() {
      if (newTodo.value.trim() === "") return;
      const newId =
        todos.value.length > 0 ? todos.value[todos.value.length - 1].id + 1 : 1;
      todos.value.push({
        id: newId,
        item: newTodo.value.trim(),
        completed: false,
        time: new Date().toLocaleTimeString([], {
          hour: "2-digit",
          minute: "2-digit",
        }),
      });
      newTodo.value = "";
    }

    function removeTodo(todoId) {
      todos.value = todos.value.filter((todo) => todo.id !== todoId);
    }

    function toggleCompletion(todo) {
      todo.completed = !todo.completed;
    }

    return {
      todos,
      newTodo,
      filter,
      filteredTodos,
      addTodo,
      removeTodo,
      toggleCompletion,
    };
  },
};
</script>

<style>
/* Add any global styles here */
</style>
