<template>
  <div id="app">
    <container />
  </div>
</template>

<script>
import Container from "./components/Container";

export default {
  name: "App",
  components: {
    Container,
  },
};
</script>

<style>
body {
  padding: 50px 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: linear-gradient(90deg, #b1a296, #d8d0ca);
  background-repeat: no-repeat;
}
</style>
