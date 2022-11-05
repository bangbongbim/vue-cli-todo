<template>
  <div id="app">

    <!-- 애플리케이션 이름 표시-->
    <TodoHeader></TodoHeader>
    <!-- 할일 입력 및 추가-->
    <!-- 하위 컴포넌트로 이벤트 전달-->
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <!-- 할 일 목록 표시 및 특정 할 일 삭제-->
    <!-- list bind-->
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <!--할 일 모두 삭제-->
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  data(){
    return{
      todoItems:[]
    }
  },
  methods:{
    addTodo(todoItem){
      localStorage.setItem(todoItem,todoItem)
      this.todoItems.push(todoItem)
    },
    removeTodo(todoItem,index){
            localStorage.removeItem(todoItem)
            this.todoItems.splice(index,1)
    }
  },
  created(){
        if(localStorage.length>0){
            for(var i = 0 ; i<localStorage.length;i++){
                this.todoItems.push(localStorage.key(i))
            }
        }
    },
   


  components:{
    "TodoHeader":TodoHeader,
    "TodoInput":TodoInput,
    "TodoList":TodoList,
    "TodoFooter":TodoFooter
  }
}
</script>


<style>
body {
  text-align: center;
  background: #f6f6f8;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.3);
}
</style>
