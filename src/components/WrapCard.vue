<template>
  <section class="wrap-card">
    <div :class="columnClass" v-for="(col, index) in colsArray" :key="index">
      <PostCard
        v-for="card in col"
        :key="card.id"
        :title="card.title"
        :body="card.body"
        :username="card.userName"
      />
    </div>
  </section>
</template>

<script>
  import PostCard from './PostCard.vue'

  export default {
    name: 'WrapCard',

    components: {
      PostCard,
    },

    props: {
      posts: {
        type: Array,
        default: () => [],
      },

      userMap: {
        type: Object,
        default: () => ({}),
      },
    },

    data() {
      return {
        cols: 3,
      }
    },

    mounted() {
      this.setCols()
      window.addEventListener('resize', this.setCols)
    },

    beforeDestroy() {
      window.removeEventListener('resize', this.setCols)
    },

    computed: {
      postProxy() {
        return this.posts.map((post) => {
          const userName = this.userMap[post.userId]

          return {
            ...post,
            userName,
          }
        })
      },

      colsArray() {
        const result = []

        for (let i = 0; i < this.cols; i++) {
          result.push([])
        }

        this.postProxy.forEach((post, index) => {
          const colIndex = index % this.cols
          result[colIndex].push(post)
        })

        return result
      },

      columnClass() {
        return `wrap-card__col-${this.cols}`
      },
    },

    methods: {
      setCols() {
        if (window.matchMedia('(min-width: 720px)').matches) {
          this.cols = 3
        } else if (window.matchMedia('(min-width: 520px)').matches) {
          this.cols = 2
        } else {
          this.cols = 1
        }
      },
    },
  }
</script>

<style lang="scss">
  .wrap-card {
    display: flex;
    flex-wrap: wrap;

    &__col-3 {
      width: calc(100% / 3);
      padding: 0 10px;
    }

    &__col-2 {
      width: calc(100% / 2);
      padding: 0 10px;
    }

    &__col-1 {
      width: 100%;
      padding: 0 10px;
    }
  }
</style>
