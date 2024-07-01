<template>
  <div class="p-3 flex justify-around">
    <input
      type="text"
      placeholder="Enter task here"
      class="p-3 focus:outline-none w-[90%] border border-slate-400"
      v-model="inputText"
    />
    <button
      @click="addItem"
      class="w-[90px] h-[50px] bg-[#2ecc71] text-white text-xl rounded-md"
    >
      Add Todo
    </button>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "TodoInput",
  props: {
    handler: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    const inputText = ref("");

    const addItem = () => {
      if (inputText.value.trim() !== "") {
        props.handler(inputText.value);
        inputText.value = "";
      }
    };

    return {
      inputText,
      addItem,
    };
  },
};
</script>
