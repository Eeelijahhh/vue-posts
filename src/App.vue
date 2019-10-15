<template>
  <div id="app">
    <PostForm />
    <form class="limit-form" @submit.prevent="submitHandler">
      <input class="limit-input" type="text" placeholder="Enter limit of posts" v-model="limit">
      <button class="limit-btn" type="submit">Change</button>
    </form>
    <h1>{{ postsCount }}</h1>
    <div 
      class="post"
      v-for="post of validPosts"
      :key="post.id"
    >
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>

<script>
import {mapGetters, mapActions} from 'vuex'
import PostForm from './components/PostForm'

export default {
  name: 'app',
  data() {
    return {
      limit: undefined
    }
  },
  components: { PostForm },
  computed: mapGetters(['validPosts', 'postsCount']),
  methods: {
    ...mapActions(['fetchPosts']),
    submitHandler() {
      this.fetchPosts(this.limit)
      this.limit = ''
    }
  },
  mounted() {
    this.fetchPosts(this.limit)
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 5rem auto;
  width: 500px;
}

.post {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 1rem;
  margin-bottom: 1rem;
}

.limit-form {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

.limit-input {
  border: 1px solid #ccc;
  border-radius: 2px;
  padding: .5rem;
  margin-bottom: 1rem;
}

.limit-btn {
  width: 100px;
  height: 33px;
}
</style>
