<template>
  <form action="">
    <label for="title">Title:</label>
    <input id="title" name="title" />

    <label for="details">Details:</label>
    <textarea name="details" id="details" cols="30" rows="10"></textarea>

    <button type="submit">Submit</button>
  </form>
</template>

<script lang="ts">
import { ref, defineComponent } from "vue";
export default defineComponent({
  name: "HelloWorld",
  props: {
    inputObj: {
      title: String,
      details: String,
      type: String,
      required: true,
    },
  },
  setup: () => {
    const count = ref(0);
    return { count };
  },
});
</script>
