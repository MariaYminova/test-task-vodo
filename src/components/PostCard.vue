<template>
  <div class="post-card">
    <div class="post-card__heading">{{ title }}</div>
    <p class="post-card__text">{{ body }}</p>
    <div class="post-card__author">{{ username }}</div>
  </div>
</template>

<script>
  export default {
    name: 'PostCard',

    props: {
      title: {
        type: String,
        default: '',
      },
      body: {
        type: String,
        default: '',
      },
      username: {
        type: String,
        default: '',
      },
    },
  }
</script>

<style lang="scss">
  .post-card {
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
