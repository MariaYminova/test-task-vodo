<template>
  <button class="search-btn">
    <img class="search-btn__icon" src="./icons/icon-search.svg" alt="#" />
  </button>
</template>

<script>
export default {
  name: "SearchBtn",
};
</script>

<style lang="scss">

.search-btn {
  height: 30px;
  width: 30px;
  padding: 5px;
  background-color: #fff;
  border: 1px solid #c9c8c8;
  border-radius: 5px 0 0 5px;

  &__icon {
    height: 15px;
    width: 15px;
  }
}
</style>
