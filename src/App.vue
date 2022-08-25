<template>
  <div>
      <div id="header">
        <SearchItem v-on:query-change="querySearch"/>
      </div>
      <div id="main-container">
        <h2>Todos</h2>
        <TodoAdd v-on:add-todo="addTodo"/>
        <TodoAll v-bind:todoslist="copyTodos" v-on:delete-todo="deleteTodo"/>
      </div>
  </div>
</template>

<script>
import TodoAll from './components/TodoAll.vue'
import TodoAdd from './components/TodoAdd.vue';
import SearchItem from './components/SearchItem.vue';

export default {
  name: 'App',
  components: {
    TodoAll,
    TodoAdd,
    SearchItem
},
  methods:{
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id != id);
      this.copyTodos = [...this.todos];
    },
    addTodo(todo){
      this.todos.push(todo);
      this.copyTodos = [...this.todos];
    },
    querySearch(query){
      if(query.trim() === ''){
        this.copyTodos =[...this.todos];
      } else{
        const temp = this.todos.filter(todo =>{
          return todo.title.toLowerCase().includes(query)
        });
        this.copyTodos = [...temp]
      }
    }
  },
  data(){
    return{
      todos: [
        {
          id: 0,
          title:  'Cocinar la cena',
          completed: false
        },
        {
         id: 1,
         title: 'Sacar a pasear a Pietra',
         completed: true
       },
       {
         id: 2,
         title: 'Estudiar',
         completed: false
       },
       {
         id: 3,
         title: 'Comprar regalo de madre',
         completed: true
       },
       {
         id: 4,
         title: 'Comprar regalo del niñe',
         completed: true
       }
      ],
      copyTodos: []
    }
  },
  created(){
    this.copyTodos = [...this.todos];
  }
 }
</script>

<style>
 *{
    box-sizing: border-box;
  }
  body{
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1.5em;
    padding: 0;
    margin: 0;
  }
  #main-container{
    border: solid 1px #ccc;
    width: 600px;
    margin: 100px auto;
    padding: 30px;
  }
  #header{
    background: black;
    padding: 10px;
  }
  h2{
    padding: 0 10px;
  }
</style>
