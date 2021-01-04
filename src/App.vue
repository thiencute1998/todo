<template>
  <div id="app">
    <Header/>
    <TodoList/>
  </div>
</template>

<script>
import TodoList from "./components/TodoList";
import Header from '@/components/header.vue'
export default {
  name: 'App',
  components : {
      TodoList,
      Header
  },

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
*{
    box-sizing: border-box;
}
</style>
