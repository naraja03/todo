<template>
  <div class="mainPage">
    <div class="main">
      <div class="top">
        <h1 class="heading">TODO</h1>
        <form @submit.prevent="addTodo()" class="todoBox">
          <div class="newTodo">
            <div class="clearAll">
              <button class="unSelect"></button>
            </div>
            <div class="input">
              <input type="text" class="border" v-model="newTodo" autofocus />
            </div>
            <div class="deleteBtn unSelect"></div>
          </div>
        </form>
        <div class="todos">
          <div
            class="todo"
            v-for="(todo, index) in todos"
            :key="todo.isCompleted"
          >
            <button class="unSelect"></button>
            <h3
              @click="todoComplete(todo, index)"
              v-bind:class="{ cut: todo.isCompleted }"
            >
              {{ todo.text }}
            </h3>
            <button class="unSelect deleteBtn"></button>
          </div>
        </div>
        <div class="footer">
          <div class="count">5 Items Left</div>
          <div class="filter">
            <div class="all">All</div>
            <div class="active">Active</div>
            <div class="completed">Completed</div>
          </div>
          <div class="clear" @click="clearAll()">Clear Completed</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "Main",
  setup() {
    let newTodo = ref();
    let todos = ref([]);

    function addTodo() {
      console.log(newTodo.value);
      if (newTodo.value.trim()) {
        todos.value.push({
          id: Date.now(),
          text: newTodo.value,
          isCompleted: false,
        });
        newTodo.value = "";
      }
    }

    function todoComplete(todo) {
      todo.isCompleted = !todo.isCompleted;
      console.log(todo.isCompleted);
      console.log(todo.index);
    }
    function clearAll(){
      todos.value=[];
    }
    return {
      newTodo,
      todos,
      addTodo,
      todoComplete,
      clearAll
    };
  },
};
</script>

<style scoped>
.cut {
  text-decoration: line-through;
  text-decoration-style:solid ;
  text-decoration-thickness:3px ;
}
.main {
  width: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;

  align-self: center;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
.unSelect {
  background: url(../assets/unselect.svg);
  width: 30px;
  height: 30px;
  background-position-x: center;
  background-position-y: center;
  border: hidden;
  margin-left: 10px;
  margin-right: 30px;
}
.newTodo {
  background-color: white;
  width: 500px;
  height: 50px;
  display: flex;
  align-items: center;
  border-radius: 8px;
}
input {
  outline: hidden;
  border: hidden;
  height: 30px;
  width: 300px;
  margin-left: 20px;
  font-size: 20px;
}
input:focus {
  outline: none;
}
.footer {
  display: flex;
  justify-content: space-around;
  background-color: white;
  width: 500px;
  height: 60px;
  border-bottom: rgba(0, 0, 0, 0.308) solid 2px;
  border-radius: 10px;
}
.filter {
  display: flex;
  justify-content: space-between;
}
.all,
.active,
.completed {
  padding: 0 10px 0 5px;
}
.todo {
  display: flex;
  align-items: center;
  border-bottom: rgba(0, 0, 0, 0.308) solid 2px;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
  width: 500px;
}
.mainPage {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: orange;
}
.top {
  width: 500px;
}
.todos {
  width: 500px;
  background: white;
  border-radius: 10px;
  margin-top: 20px;
  cursor: pointer;
}
.deleteBtn{
  margin-left: auto;
  margin-right: 10px;
}
</style>
