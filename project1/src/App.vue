<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>

import axios from 'axios';
import AddTodo from './components/AddTodo';
import Todos from './components/Todos';
import Header from './components/Layout/Header';
export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data(){
    return{
      todos:[]
    }
  },
  methods:{
    deleteTodo(id){
      this.todos=this.todos.filter(todo=> todo.id !== id);
    },
    addTodo(newTodo){
      const{title, completed}= newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
        .then(res=>this.todos=[...this.todos, res.data])
        .catch(err=>console.log(err))
      
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos')
    .then(res => this.todos= res.data)
    .catch(err=>console.log(err))
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.btn{
  display:inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover{
  background: #666;
}
</style>
