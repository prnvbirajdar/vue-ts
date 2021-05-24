<template>
  <h1>Todo List (Vue + TS)</h1>

  <h2>Search</h2>

  <label for="search">
    <input id="search" name="search" v-model="searchInput" />
  </label>

  <h2>Add Todo</h2>

  <form @submit.prevent="addTodo">
    <div>
      <label for="title">Title:</label>
      <input id="title" name="title" v-model.trim.lazy="title" />
    </div>

    <div>
      <label for="details">Details:</label>
      <textarea
        name="details"
        id="details"
        cols="30"
        rows="2"
        v-model.trim.lazy="details"
      />
    </div>

    <button type="submit">Submit</button>
  </form>
  <ul>
    <li v-for="(todo, index) in filteredTodos" :key="todo.id">
      <div :class="{ done: todo.completed }">
        {{ todo.title }}
        <label for="todoCompleted">
          <input
            type="checkbox"
            name="todoCompleted"
            id="todoCompleted"
            v-model="todo.completed"
          />
        </label>
      </div>
      <div :class="{ done: todo.completed }">
        {{ todo.details
        }}<button type="button" @click="removeTodo(index)">X</button>
      </div>
      <br />
      <hr />
    </li>
  </ul>

  <!-- <FormInput inputObj="inputData" /> -->
</template>

<script lang="ts">
import { defineComponent, reactive, toRefs, ref, computed } from "vue";
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

    const searchInput = ref("");

    const todos = reactive<Todos[]>([
      {
        title: "one",
        details: "details",
        id: 1,
        completed: true,
      },
      {
        title: "two",
        details: "details2222",
        id: 2,
        completed: false,
      },
      {
        title: "three",
        details: "details3333333",
        id: 3,
        completed: false,
      },
    ]);

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

    const filteredTodos = computed(() => todos.filter((todo) => todo.title.includes(searchInput.value)));

    return {
      ...toRefs(inputData),
      addTodo,
      todos,
      removeTodo,
      searchInput,
      filteredTodos,
    };
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

.done {
  text-decoration: line-through;
  color: green;
}
</style>
