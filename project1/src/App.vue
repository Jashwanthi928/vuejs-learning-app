<template>
  <div id="app">
    <Header/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>

import Todos from './components/Todos';
import Header from './components/Layout/Header';
export default {
  name: 'App',
  components: {
    Todos,
    Header
  },
  data(){
    return{
      todos:[
        {
          id:1,
          title:"Todo One",
          completed:false
        },
        {
          id:2,
          title:"Todo Two",
          completed:true
        },
        {
          id:3,
          title:"Todo Three",
          completed:false
        }
      ]
    }
  },
  methods:{
    deleteTodo(id){
      this.todos=this.todos.filter(todo=> todo.id !== id);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
