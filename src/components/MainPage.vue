<template> 
  <div>
    <div class="btn-search">
      <SearchBtn @click="fetchPosts(searchAuthor)" />
      <SearchSelect v-model="searchAuthor" />
    </div>

    <div v-if="notFound">"{{ searchAuthor }}" author has not been found</div>
    <div class="grid">
      <div class="grid__col" v-for="(col, index) in colsArray" :key="index">
        <Card
          v-for="card in col"
          :key="card.id"
          :title="card.title"
          :body="card.body"
          :username="getUserName(card.userId)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
import SearchSelect from "./SearchSelect.vue";
import SearchBtn from "./SearchBtn.vue";

export default {
  name: "MainPage",

  components: {
    Card,
    SearchSelect,
    SearchBtn,
  },

  data() {
    return {
      posts: [],
      users: [],
      cols: 3,
      searchAuthor: "",
      notFound: false,
    };
  },

  created() {
    this.fetchPosts();
    this.getUsers();
  },

  mounted() {
    this.setCols();
    window.addEventListener("resize", this.setCols);
  },

  beforeDestroy() {
    window.removeEventListener("resize", this.setCols);
  },

  computed: {
    colsArray() {
      const result = [];

      for (let i = 0; i < this.cols; i++) {
        result.push([]);
      }

      this.posts.forEach((post, index) => {
        const colIndex = index % this.cols;
        result[colIndex].push(post);
      });

      return result;
    },
  },

  methods: {
    async getUsers() {
      try {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users`
        );

        this.users = await response.json();
      } catch (error) {
        console.error("Failed to fetch users:", error);
      }
    },

    getUserName(userId) {
      const user = this.users.find((user) => user.id === userId);
      return user ? user.name : "";
    },

    setCols() {
      if (window.matchMedia("(min-width: 720px)").matches) {
        this.cols = 3;
      } else {
        this.cols = 2;
      }
    },

    async fetchPosts(searchAuthor) {
      searchAuthor = this.searchAuthor.trim();

      if (searchAuthor) {
        const user = this.users.find((user) =>
          user.name.includes(searchAuthor)
        );

        if (user) {
          const response = await fetch(
            `https://jsonplaceholder.typicode.com/posts?userId=${user.id}`
          );
          this.posts = await response.json();
          this.notFound = false;
        } else {
          this.notFound = true;
          this.posts = [];
        }
      } else {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/posts`
        );
        this.posts = await response.json();
        this.notFound = false;
      }
    },
  },
};
</script>

<style lang="scss">
.btn-search {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
}

.grid {
  display: flex;
  flex-wrap: wrap;

  &__col {
    width: calc(100% / 3);
    padding: 0 10px;

    @media (max-width: 720px) {
      width: calc(100% / 2);
    }

    @media (max-width: 540px) {
      width: 100%;
    }
  }
}
</style>
