<template>
  <div class="bg">
    <div class="main shadow">
      <h1>TODO</h1>
      <form @submit.prevent="addTodo">
        <div class="newTodo">
          <div class="mouse"
            :class="{
              unSelect: (todos.done = true),
              select: (todos.done = true),
            }"
            @click="completeAll"
          ></div>

          <input
            type="text"
            name="todo"
            id="todo"
            placeholder="Enter Todo Title"
            v-model="newTodo"
            ref="auto"
          />
          <div class="unSelect mouse" @click="removeAll"></div>
        </div>
      </form>
      <hr />
      <div class="todos shadow">
        <div class="todo" v-for="(todo, index) in todos" :key="todo.done">
          <div class="mouse"
            :class="{
              unSelect: (todos.done = false),
              select: (todos.done = true),
            }"
            @click="todoFinish(todo)"
          ></div>
          <h2 :class="{ done: todo.done }" @click="todoFinish(todo)" class="content mouse ">
            {{ todo.content }}
          </h2>
          <div class="unSelect mouse" @click="removeTodo(index)"></div>
        </div>
      </div>
      <div class="footer">
        <div class="button mouse">{{ todos.length }} todos</div>
        <!-- <div class="filter">
          <div class="all button">All</div>
          <div class="active button">Active</div>
          <div class="complete button">Complete</div>
        </div> -->
        <div @click="removeAll" class="mouse button">Clear All</div>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
export default {
  name: "App",
  components: {},
  setup() {
    let newTodo = ref("");
    let todos = ref([]);
    let auto = ref(null);

    onMounted(() => auto.value.focus());
    function addTodo() {
      console.log(newTodo.value);
      if (newTodo.value.trim()) {
        todos.value.push({
          done: false,
          content: newTodo.value,
        });
      }

      newTodo.value = "";
    }
    function todoFinish(todo) {
      todo.done = !todo.done;
      console.log(todo.done);
    }
    function removeTodo(index) {
      todos.value.splice(index, 1);
    }
    function completeAll() {
      todos.value.forEach((todo) => (todo.done = !todo.done));
    }
    function removeAll() {
      todos.value = [];
    }

    return {
      removeAll,
      addTodo,
      newTodo,
      auto,
      todos,
      todoFinish,
      removeTodo,
      completeAll,
    };
  },
};
</script>

<style scoped>
.content {
  height: auto;
  word-wrap: break-word;
  width: 350px;
}
.bg {
  background: url(../assets/background.jpg);
  height: 300px;
  margin: 0;
  padding: 15px;
}
.done {
  text-decoration: line-through;
  text-decoration-style: solid;
  text-decoration-thickness: 3px;
}
.h1 {
  text-align: left;
}
.main {
  margin-top: 30px;
  width: 600px;
  border-radius: 10px;
  display: flex;
  /* justify-content: center; */
  align-items: center;
  margin: auto;
  flex-flow: column;
  align-self: center;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  background-color: rgba(255, 255, 255, 0.247);
  text-transform: uppercase;
}
.main:hover {
  box-shadow: 0px 0px 75px 10px rgba(0, 0, 0, 0.521);
  padding: 5px;
  border-radius: 10px;
}
.button {
  background-color: rgba(255, 255, 255, 0.247);
  padding: 10px;
  border-radius: 10px;
  margin: 0 auto;
}
.unSelect {
  background: url(../assets/uncheck.png);
  width: 30px;
  height: 30px;
  background-position-x: center;
  background-position-y: center;
  border: hidden;
  margin-left: 10px;
  margin-right: 30px;
}
.select {
  background: url(../assets/check.png);
  width: 28px;
  height: 28px;
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
  justify-content: space-around;
  border-radius: 8px;
}
input {
  outline: hidden;
  border: hidden;
  height: 30px;
  width: 300px;
  margin-left: 20px;
  font-size: 20px;
  background-color: white;
}
input:focus {
  outline: none;
}
.footer {
  display: flex;
  justify-content: space-around;
  align-items: center;
  background-color: black;
  color: white;
  width: 500px;
  height: 60px;
  border-bottom: rgba(0, 0, 0, 0.308) solid 2px;
  border-radius: 10px;
  margin-bottom: 20px;
}
.filter {
  display: flex;
  justify-content: space-between;
  /* align-items: center; */
}
.all,
.active,
.completed {
  margin: 0 4px;
}
.todo {
  display: flex;
  justify-content: space-around;
  align-items: center;
  border-bottom: rgba(0, 0, 0, 0.308) solid 2px;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
  width: 500px;
}
.todoStyle {
  text-transform: uppercase;
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
}
.deleteBtn {
  margin-left: auto;
  margin-right: 10px;
}
.mouse {
  cursor: pointer;
}
.shadow {
  box-shadow: 0px 0px 47px 5px rgba(0, 0, 0, 0.521);
}
</style>
