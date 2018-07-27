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
      todos: [],
      lastKey:0
    }
  },
  methods:{
    todoAdd:function(todoText) {
      this.lastKey = this.lastKey+1;
      var todo = { "title" : todoText, "done" : false,"key":"key"+this.lastKey}
      this.todos.push(todo)
      this.setItem(todo)
    },
    todoDelete:function(todo){
      localStorage.removeItem(todo.key)
      this.todos.splice(this.todos.indexOf(todo),1)
    },
    todoClear:function(){
      this.todos=[]
      this.lastKey = 0;
      localStorage.clear()
    },
    todoDone:function(todo){
      this.setItem(todo)
    },
    setItem:function(todo){
      var strTodo=JSON.stringify(todo)
      localStorage.setItem(todo.key,strTodo)
    }
  },
  created(){
    if(localStorage.length>0){
      for(var i=0; i<localStorage.length; i++){
        var key =localStorage.key(i)
        if(key =="loglevel:webpack-dev-server"){
          continue;
        }
        var data = JSON.parse(localStorage.getItem(key))
        this.todos.push(data)
        this.lastKey =data.key.split("key")[1]
        
      }
    }
  }
}
</script>

<style>

</style>
