<template>
  <div
    @click="toggleDone"
    class="select-none cursor-pointer w-full border-b p-3 flex justify-between items-center"
  >
    <div>
      <span class="pr-2 text-[14px] text-slate-400">{{ time }}</span>
      <span :class="{ 'line-through': done }" class="text-[20px]">{{
        item
      }}</span>
    </div>
    <div @click.stop="removeItem">
      <DeleteIcon class="text-[#e74c3c]" />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import DeleteIcon from "@mui/icons-material/Delete";

export default {
  name: "TodoItem",
  components: {
    DeleteIcon,
  },
  props: {
    id: {
      type: Number,
      required: true,
    },
    item: {
      type: String,
      required: true,
    },
    time: {
      type: String,
      required: true,
    },
    removeHandler: {
      type: Function,
      required: true,
    },
  },
  setup(props) {
    const done = ref(false);

    const toggleDone = () => {
      done.value = !done.value;
    };

    const removeItem = () => {
      props.removeHandler(props.id);
    };

    return {
      done,
      toggleDone,
      removeItem,
    };
  },
};
</script>

<style scoped>
/* Add scoped styles if necessary */
</style>
