<template>
<v-layout justify-center column>
    <v-list>
          <v-list-tile
            v-for="(todo, index) in toDoItems"
            :key="index"
            @click=""
          >
            <v-list-tile-action @click="todoDone(todo,index)">
               <v-checkbox v-model="todo.done"></v-checkbox>
            </v-list-tile-action>

            <v-list-tile-content>
              <v-list-tile-title v-bind:style="[todo.done ? doneStyle : '']">{{todo.title}}</v-list-tile-title>
            </v-list-tile-content>
            
            <v-list-tile-action>
             <v-icon color="red" @click="todoDelete(todo)">delete</v-icon>
            </v-list-tile-action>
          </v-list-tile>
        </v-list>
</v-layout>
</template>

<script>
export default {
    name:'ToDoList',
    props:{
        toDoItems:Array
    },
    data(){
        return{
            doneStyle:{
                'text-decoration-line': 'line-through'
            }
        }
    },
    methods:{
        todoDelete:function(todo){
            this.$emit("todoDelete",todo)
        },
        todoDone(todo){
            this.$emit("todoDone",todo)
        }
    }
}
</script>

<style>


</style>

