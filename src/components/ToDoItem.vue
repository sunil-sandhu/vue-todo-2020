<template>
  <div class="ToDoItem">
    <p class="ToDoItem-Text">{{item.text}}</p>
    <button class="ToDoItem-Delete" @click="deleteItem(item.id)">-</button>
  </div>
</template>

<script>
export default {
  name: "ToDoItem",
  props: ["item"],
  setup(props, { emit }) {
    function deleteItem(id) {
      emit("delete", id);
    }
    return {
      deleteItem
    };
  }
};
</script>

<style>
.ToDoItem {
  display: flex;
  justify-content: center;
  align-items: center;
}

.ToDoItem-Text {
  width: 90%;
  padding: 12px;
  margin-right: 10px;
  border-radius: 4px;
  border-color: rgba(0, 0, 0, 0.5);
  background: #ffffff;
  box-shadow: 5px 5px 13px #d9d9d9, -5px -5px 13px #ffffff;
  text-align: left;
}

.ToDoItem-Delete {
  width: 50px;
  height: 50px;
  border-radius: 10px;
  background: linear-gradient(145deg, #e6e6e6, #ffffff);
  box-shadow: 5px 5px 15px #cccccc, -5px -5px 15px #ffffff;
  border-color: transparent;
  color: red;
  font-size: 2rem;
  cursor: pointer;
}

.ToDoItem-Delete:hover {
  box-shadow: 5px 5px 10px #cccccc, -5px -5px 10px #ffffff;
}
</style>