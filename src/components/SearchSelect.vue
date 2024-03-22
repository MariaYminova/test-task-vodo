<template>
  <input
    class="search-select"
    type="text"
    placeholder=" Filter by author..."
    v-model="author"
  />
</template>

<script>
export default {
  name: "SearchSelect",

  data() {
    return {
      author: "",
    };
  },

  computed: {
    searchAuthor() {
      return this.author;
    },
  },

  watch: {
    author(newValue) {
      this.$emit("update:searchAuthor", newValue);
    },
  },
};
</script>

<style lang="scss">
.search-select {
  width: 300px;
  padding: 5px;
  border: 1px solid #c9c8c8;
  border-radius: 0 5px 5px 0;

  @media (max-width: 540px) {
    width: 85%;
  }
}
</style>
