<template>
<v-layout>
   <v-flex xs12><v-text-field placeholder='할일을 입력해주세요.' v-model="inputText" @keyup.enter="todoAdd"></v-text-field></v-flex>
   <v-flex p>
   <v-btn color="success" @click="todoAdd">추가</v-btn>
   </v-flex>
   <v-flex p>
   <v-btn color="success" @click="todoClear">모두삭제</v-btn>
   </v-flex>
</v-layout>
</template>

<script>

export default {
    name:'ToDoInputArea',
    data(){
        return{
            inputText:''
        }
    },
    methods:{
       todoAdd:function(){
          if(this.inputText.trim()==''){
            alert("할일을 입력해주세요.")
            return
          }
           this.$emit('todoAdd',this.inputText);
           this.inputText='';
       },
       todoClear:function(){
           this.$emit('todoClear');
       }
    }

}
</script>

<style>

</style>
