<template>
  <div id="app">
    <ToDo />
  </div>
</template>

<script>
import ToDo from "./components/ToDo.vue";

export default {
  name: "app",
  components: {
    ToDo
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, Helvetica,
    Arial, sans-serif;
  height: auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgb(255, 171, 208);
  background: linear-gradient(135deg, rgb(255, 237, 171), rgb(234, 121, 170));
}

input {
  width: 90%;
  padding: 10px;
  font-size: 1em;
  margin: 10px 10px 10px auto;
  border-radius: 4px;
  padding: 12px;
  border-color: rgba(0, 0, 0, 0.1);
  background: #ffffff;
  box-shadow: 5px 5px 13px #d9d9d9, -5px -5px 13px #ffffff;
}
</style>
