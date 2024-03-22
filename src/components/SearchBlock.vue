<template>
  <form @submit.prevent="handleSubmit">
    <div class="search-block">
      <button class="search-block__btn" type="submit">
        <img
          class="search-block__icon"
          src="../assets/icons/icon-search.svg"
          alt="#"
        />
      </button>
      <input
        class="search-block__select"
        type="text"
        placeholder=" Filter by author..."
        v-model="value"
      />
    </div>
  </form>
</template>

<script>
  export default {
    name: 'SearchBlock',

    data() {
      return {
        value: '',
      }
    },

    methods: {
      handleSubmit() {
        this.$emit('search', this.value)
      },
    },
  }
</script>

<style lang="scss">
  .search-block {
    display: flex;
    justify-content: center;

    &__select {
      width: 300px;
      padding: 5px;
      border: 1px solid #c9c8c8;
      border-radius: 0 5px 5px 0;

      @media (max-width: 540px) {
        width: 250px;
      }
    }

    &__btn {
      height: 30px;
      width: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      background-color: #fff;
      border: 1px solid #c9c8c8;
      border-radius: 5px 0 0 5px;
    }

    &__icon {
      height: 15px;
      width: 15px;
    }
  }
</style>
