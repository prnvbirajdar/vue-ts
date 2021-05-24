<template>
  <h1>Todo List (Vue + TS)</h1>

  <FormInput inputObj="inputData" />
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import FormInput from "./components/FormInput.vue";

export default defineComponent({
  name: "App",
  components: {
    FormInput,
  },
  setup() {
    const inputData = ref({
      id: Date.now(),
      title: "",
      details: "",
      completed: false
    });

    return { inputData };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
