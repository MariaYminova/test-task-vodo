<template>
  <div class="container">
    <MainPage />
  </div>
</template>

<script>
import MainPage from "./components/MainPage.vue";

export default {
  name: "App",

  components: {
    MainPage,
  },
};
</script>

<style lang="scss">

.container {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
