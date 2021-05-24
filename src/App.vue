<template>
  <h1>Todo List (Vue + TS)</h1>

  <form @submit.prevent="addTodo">
    <div>
      <label for="title">Title:</label>
      <input id="title" name="title" v-model="title" />
    </div>

    <div>
      <label for="details">Details:</label>
      <textarea
        name="details"
        id="details"
        cols="30"
        rows="10"
        v-model="details"
      />
    </div>

    <button type="submit">Submit</button>
  </form>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id">
      <div>
        {{ todo.title }}
        <button type="button" @click="removeTodo(index)">X</button>
      </div>
      <div>{{ todo.details }}</div>
    </li>
  </ul>

  <!-- <FormInput inputObj="inputData" /> -->
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs } from "vue";
import FormInput from "./components/FormInput.vue";
import Todos from "./types/todos";

export default defineComponent({
  name: "App",
  components: {
    FormInput,
  },
  setup() {
    const inputData = reactive({
      title: "",
      details: "",
    });

    const todos = reactive<Todos[]>([]);

    const addTodo = () => {
      todos.push({
        title: inputData.title,
        details: inputData.details,
        id: Date.now(),
        completed: false,
      });
      inputData.title = "";
      inputData.details = "";
    };

    const removeTodo = (i: number) => {
      todos.splice(i, 1);
    };

    return { ...toRefs(inputData), addTodo, todos, removeTodo };
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
