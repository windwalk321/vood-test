<template>
  <div
    id="app"
    class="container-fluid pt-5 app"
  >
    <div class="row justify-content-center mb-4 ">
      <app-input v-model="searchQuery" />
    </div>

    <div
      class="d-flex align-items-center"
      v-if="loading"
    >
      <strong class="text-primary">Loading...</strong>
      <div
        class="spinner-border ml-auto text-primary"
        role="status"
        aria-hidden="true"
      ></div>
    </div>

    <div
      class="card-columns app__posts"
      v-else
    >
      <app-posts-item
        v-for="post in filteredPosts"
        :key="post.id"
        :post="post"
      />
    </div>
  </div>
</template>

<script>
import appInput from './components/app-input'
import appPostsItem from './components/app-posts-item'

import axios from 'axios'

export default {
  name: 'App',
  components: {
    appInput,
    appPostsItem
  },
  data () {
    return {
      posts: [],
      users: [],
      rightPosts: [],
      searchQuery: '',
      loading: true
    }
  },
  computed: {
    filteredPosts () {
      if (this.searchQuery.trim().length > 0) {
        return this.rightPosts.filter(post => {
          return post.author.name.toLowerCase().includes(this.searchQuery.toLowerCase())
        })
      }
      return this.rightPosts
    }
  },
  methods: {
    getDataFromApi (type) {
      const apiUrl = 'https://jsonplaceholder.typicode.com'

      return axios
        .get(`${apiUrl}/${type}`)
        .then(response => (this[type] = response.data))
        .catch(error => console.log(error))
    }
  },
  async mounted () {
    await this.getDataFromApi('posts')
    await this.getDataFromApi('users')

    this.rightPosts = this.posts.map(item => ({
      ...item,
      author: this.users.find(user => user.id === item.userId)
    }))
    this.loading = false
  }
}
</script>

<style lang="scss">
.app {
  height: 100%;
  padding: 3rem;
  @include media-breakpoint-only(xs) {
    padding: 0 1rem;
  }
}
.app__posts {
  @include media-breakpoint-only(md) {
    column-count: 3;
  }
  @include media-breakpoint-only(sm) {
    column-count: 2;
  }
  @include media-breakpoint-only(xs) {
    column-count: 1;
  }
}
</style>
