<template>
  <h1 style="text-align:center">todoList</h1>
  <div id="app">
    <date-bar></date-bar>
    <todo-list></todo-list>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap";
import dateBar from "./components/dateBar.vue";
import todoList from "./components/todoList.vue";

export default defineComponent({
  name: "App",
  components: {
    dateBar,
    todoList
  }
});
</script>
