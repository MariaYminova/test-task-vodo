<template>
  <SearchBlock class="btn-search" @search="fetchPosts" />

  <div v-if="errorMessage">{{ errorMessage }}</div>

  <WrapCard v-else :posts="posts" :userMap="userMap" />
</template>

<script>
  import SearchBlock from '@/components/SearchBlock.vue'
  import WrapCard from '@/components/WrapCard.vue'

  export default {
    name: 'MainPage',

    components: {
      SearchBlock,
      WrapCard,
    },

    data() {
      return {
        posts: [],
        users: [],
        userMap: {},
        errorMessage: null,
      }
    },

    created() {
      this.fetchPosts()
      this.getUsers()
    },

    methods: {
      async getUsers() {
        const response = await fetch(
          `https://jsonplaceholder.typicode.com/users`
        )

        const users = await response.json()
        const userMap = {}

        users.forEach((user) => {
          userMap[user.id] = user.name
        })

        this.users = users
        this.userMap = userMap
      },

      async fetchPosts(searchAuthor) {
        this.errorMessage = null
        let targetUser = null
        let params = ''

        try {
          if (searchAuthor) {
            searchAuthor = searchAuthor.trim().toLowerCase()

            targetUser = this.users.find((user) =>
              user.name.toLowerCase().includes(searchAuthor)
            )

            if (targetUser) {
              params = `?userId=${targetUser.id}`
            } else {
              throw false
            }
          }

          const response = await fetch(
            `https://jsonplaceholder.typicode.com/posts${params}`
          )

          const posts = await response.json()

          if (posts && posts.length) {
            this.posts = posts
          } else {
            throw false
          }
        } catch (e) {
          this.errorMessage = `"${searchAuthor}" not been found`
          this.posts = []
        }
      },
    },
  }
</script>

<style lang="scss">
  .btn-search {
    margin-bottom: 30px;
  }
</style>
