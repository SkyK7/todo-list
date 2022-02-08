<template>
  <div class="container">
    <Header />

    <todos />
  </div>
</template>

<script>
import Header from "./Header";

import Todos from './Todos';

export default {
  components: {
    Header,
    Todos,
   
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  text-align: center;
  padding: 30px 40px 20px;
  text-align: center;
  width: 440px;
  max-width: 100%;
  margin: 0 auto;
  border-radius: 15px;
  background: #f2f2f2;
}
</style>
