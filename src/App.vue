<template>
  <div class="">
    <nav-bar />
  </div>
</template>

<script>
import navBar from "./components/navbar.vue";
export default {
  name: "App",
  components: {
    navBar,
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600&display=swap");
body {
  margin: 0;
  font-family: "Inter", sans-serif;
  font-weight: 400;
}
</style>
