<template>
  <h1>Todo List (Vue + TS)</h1>

  <form @submit.prevent="addTodo">
    <label for="title">Title:</label>
    <input id="title" name="title" v-model="title" />

    <label for="details">Details:</label>
    <textarea
      name="details"
      id="details"
      cols="30"
      rows="10"
      v-model="details"
    />

    <button type="submit">Submit</button>
  </form>

  <div>{{ title }}</div>

  <div>{{ details }}</div>

  <ul>
    <li v-for="todo in todos" :key="todo.id">{{ todo.title }}</li>
  </ul>

  <!-- <FormInput inputObj="inputData" /> -->
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from "vue";
import FormInput from "./components/FormInput.vue";

export default defineComponent({
  name: "App",
  components: {
    FormInput,
  },
  setup() {
    const inputData = reactive({
      id: Date.now(),
      title: "",
      details: "",
      completed: false,
    });

    const todos = reactive([]);

    const addTodo = () => {
      console.log(inputData);
      todos.push({ inputData });
    };

    return { ...toRefs(inputData), addTodo, todos };
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
