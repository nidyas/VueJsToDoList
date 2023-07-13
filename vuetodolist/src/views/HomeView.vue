<script setup>
import { ref ,watch} from "vue";
import TodoCreator from "../components/TodoCreator.vue";
import todoItem from "../components/todoItem.vue";
import {uid} from"uid";

const todolist=ref([])
  watch( todolist,()=>{
      savelocal()
  },
  {
  deep:true}
)



//ilawej 3alli fama fe local storage
const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("list"));
  if (savedTodoList) {
    todolist.value = savedTodoList;
  }
};
//isavi kol chay fe local storage
fetchTodoList();
const savelocal=()=>{
  localStorage.setItem("list",JSON.stringify(todolist.value))
}


const createtodo=(todo)=>{
  
todolist.value.push({
  id:uid(),
  todo,
  isCompleted:null,
  isEditing:null

}

);

}

const completetodo=(position)=>{
  console.log("+++"+position)
  console.log("+++***"+todolist.value)
todolist.value[position].isCompleted=!todolist.value[position].isCompleted

}
const toggleEditTodo = (todoPos) => {
  todolist.value[todoPos].isEditing = !todolist.value[todoPos].isEditing;
 
};

const updateTodo = (todoVal, todoPos) => {
  todolist.value[todoPos].todo = todoVal;
 
};

const deleteTodo = (todo) => {
  todolist.value = todolist.value.filter(
    (todoFilter) => todoFilter.id !== todo.id
  );
  savelocal()
};


</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @add="createtodo"/>
  </main>
  <ul class="todo-list" v-if="todolist.length > 0">
      <todoItem v-for="(todo,index) in todolist" :todo="todo" :index="index" @complete="completetodo" @delete="deleteTodo" 
      @updatetext="updateTodo" @editpost="toggleEditTodo"/>
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="fa6-solid:face-sad-cry" />

      <span>You have no todo's to complete! Add one!</span>
    </p>
</template>

<style scoped lang="scss">
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }
}
</style>