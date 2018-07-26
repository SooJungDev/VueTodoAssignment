<template>
  <div id="app">
    <v-app>
  <v-content>
    <v-container align-center>
      <h1>{{title}}</h1>
      <todo-input-area @todoAdd ="todoAdd" @todoClear="todoClear"></todo-input-area>
      <todo-list :to-do-items="todos" @todoDone="todoDone" @todoDelete="todoDelete"></todo-list>
    </v-container>
  </v-content>
</v-app>
 </div>
</template>

<script>
import TodoInputArea from './ToDoInputArea.vue'
import TodoList from './ToDoList.vue' 

export default {
  name: 'app',
  components:{
    TodoInputArea,
    TodoList
  },
  data () {
    return {
      title: 'Todo App',
      todos: []
    }
  },
  methods:{
    todoAdd:function(todoText) {
      var todo={ "title" : todoText, "done" : false}
      this.todos.push(todo)
      var index= this.todos.length
      var strTodo=JSON.stringify(todo)
      localStorage.setItem("key"+index,strTodo)
    },
    todoDelete:function(index){
      localStorage.removeItem("key"+index)
      this.todos.splice(index,1)
    },
    todoClear:function(){
      this.todos=[]
      localStorage.clear()
    },
    todoDone:function(todo,index){
      var strTodo=JSON.stringify(todo)
      localStorage.setItem("key"+index,strTodo)
    }
  },
  created(){
    if(localStorage.length>0){
      for(var i=0; i<localStorage.length; i++){
        var key =localStorage.key(i)
        if(key =="loglevel:webpack-dev-server"){
          continue;
        }
        var data = localStorage.getItem(key)
        data =JSON.parse(data)
        this.todos.push(data)
        
      }
    }
  }
}
</script>

<style>

</style>
