<template>
  <main class="container">
    <MainPage />
  </main>
</template>

<script>
  import MainPage from './views/MainPage.vue'

  export default {
    name: 'App',

    components: {
      MainPage,
    },
  }
</script>

<style lang="scss">
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 40px 10px;
  }
</style>
