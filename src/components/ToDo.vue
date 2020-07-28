<template>
  <div class="ToDo">
    <img class="Logo" :src="logo" alt="Vue logo" />
    <h1 class="ToDo-Header">Vue To Do</h1>
    <div class="ToDo-Container">
      <div class="ToDo-Content">
        <ToDoItem v-for="item in list" :item="item" @delete="onDeleteItem" :key="item.id" />
      </div>
      <div class="ToDoInput">
        <input
          type="text"
          placeholder="I need to..."
          v-model="todo"
          v-on:keyup.enter="createNewToDoItem"
        />
        <button class="ToDo-Add" @click="createNewToDoItem">+</button>
      </div>
      <div class="ToDo-ErrorContainer">
        <p v-if="showError">Please enter a todo!</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import ToDoItem from "./ToDoItem.vue";
import Logo from "../assets/logo.png";

export default {
  name: "ToDo",
  components: {
    ToDoItem
  },
  setup() {
    const list = ref([
      { id: 1, text: "clean the house" },
      { id: 2, text: "buy milk" }
    ]);
    const todo = ref("");
    const logo = Logo;
    const showError = ref(false);

    function generateId() {
      if (list.value && list.value.length) {
        return Math.max(...list.value.map(t => t.id)) + 1;
      } else {
        return 1;
      }
    }

    function createNewToDoItem() {
      //validate todo
      if (!todo.value) {
        this.displayError();
        return;
      }

      const newId = generateId();
      list.value.push({ id: newId, text: todo.value });
      todo.value = "";
    }

    function onDeleteItem(id) {
      list.value = list.value.filter(item => item.id !== id);
    }

    function displayError() {
      showError.value = true;
      const clearTimer = setTimeout(() => (showError.value = false), 3000);
      return () => clearTimeout(clearTimer);
    }

    return {
      list,
      todo,
      logo,
      showError,
      generateId,
      createNewToDoItem,
      onDeleteItem,
      displayError
    };
  }
};
</script>

<style>
.Logo {
  width: 50px;
  position: relative;
  top: 50px;
}

.ToDo {
  text-align: center;
  width: 80vw;
  max-width: 768px;
  height: auto;
  margin: 40px auto;
  border-radius: 10px;
  background: #ffffff;
}

.ToDoInput {
  margin-top: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.ToDo-Header {
  color: black;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
    Arial, sans-serif;
  font-weight: 400;
  text-transform: uppercase;
  margin: 70px auto 30px;
}

.ToDo-Subheader {
  font-size: 1em;
  color: black;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
    Arial, sans-serif;
  font-weight: 400;
  margin: 4px auto 20px;
}

.ToDo-Add {
  cursor: pointer;
  width: 50px;
  height: 50px;
  border-color: transparent;
  color: #73ff73;
  font-size: 2rem;
  border-radius: 10px;
  background: linear-gradient(145deg, #e6e6e6, #ffffff);
  box-shadow: 5px 5px 15px #cccccc, -5px -5px 15px #ffffff;
}

.ToDo-Add:hover {
  box-shadow: 5px 5px 10px #cccccc, -5px -5px 10px #ffffff;
}

.ToDo-Container {
  width: 80%;
  margin: 0 auto;
}

.ToDo-ErrorContainer {
  height: 100px;
  width: 90%;
  display: flex;
  justify-content: center;
  align-items: center;
  color: red;
  font-size: 1rem;
}
</style>
