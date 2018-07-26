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
              <v-list-tile-title>{{todo.title}}</v-list-tile-title>
            </v-list-tile-content>
            
            <v-list-tile-action>
             <v-icon color="red" @click="todoDelete(index)">delete</v-icon>
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
        }
    },
    methods:{
        todoDelete:function(index){
            this.$emit("todoDelete",index)
        },
        todoDone(todo,index){
            this.$emit("todoDone",todo,index)
        }
    }
}
</script>

<style>

</style>

