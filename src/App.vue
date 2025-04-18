<template>
  <div class="app">
    <UsersManager />
  </div>
</template>

<script>
import UsersManager from "./components/users/UsersManager.vue";
export default {
  components: {
    UsersManager,
  },
};

</script>

<style>
.app {
  font-family: "Open Sans", sans-serif;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
