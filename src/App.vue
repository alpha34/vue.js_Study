<template>
    <div id="app">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
      <TodoList v-bind:propsdata="todoItems" v-on:removeTodo2="removeTodo"></TodoList>
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
    </div>
</template>

<script>
/* 싱글파일 컴포넌트(.vue 파일체계)에서는 특정 컴포넌트에서 다른위치 컴포넌트 불러올땐 import를 사용한다.  */
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  props:['propsdata'],
  data(){
    return {
      todoItems:[]
    }
  },
  created(){
      if(localStorage.length > 0){
          for(var i=0 ; i<localStorage.length ; i++){
              this.todoItems.push(localStorage.key(i));
          }
      }
  },  
  methods: {
    addTodo(todoItem){
      //로컬 스토리지에 데이터를 추가하는 로직
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    }
  },
  components :{
    'TodoHeader':TodoHeader,
    'TodoInput':TodoInput,
    'TodoList':TodoList,
    'TodoFooter':TodoFooter,
  }
}

</script>

<style>
  body{
      text-align: center;
      background-color: #f6f6f8;
  }
  input{
      border-style: groove;
      width: 200px;
  }
  button{
      border-style: groove;
  }
  .shadow{
      box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
  }
</style>