<template>
  <div class="card">
    <div class="card__heading">{{ title }}</div>
    <div class="card__text">{{ body }}</div>
    <div class="card__author">{{ username }}</div>
  </div>
</template>

<script>
export default {
  name: "Card",

  props: {
    title: String,
    body: String,
    username: String,
  },
};
</script>

<style lang="scss">
.card {
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 5px;
  background-color: #fff;
  box-shadow: 0px 1px 2px #0000005c;

  &__heading {
    color: #6596e0;
    margin-bottom: 10px;
  }

  &__text {
    color: #454647;
    margin-bottom: 15px;
  }

  &__author {
    color: #999a9b;
  }
}
</style>
