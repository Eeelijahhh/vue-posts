<template>
  <form @submit.prevent="submitHandler">
    <input type="text" placeholder="Title" v-model="title">
    <input type="text" placeholder="Body" v-model="body">
    <button type="submit">Create Post</button>
  </form>
</template>

<script>
import { mapMutations } from 'vuex'

export default {
  data() {
    return {
      title: '',
      body: ''
    }
  },
  methods: {
    ...mapMutations(['createPost']),
    submitHandler() {
      this.createPost({
        title: this.title,
        body: this.body,
        id: Date.now()
      })
      this.title = this.body = ''
    }
  }
}
</script>

<style scoped>
  input {
    display: block;
    width: 100%;
    border: 1px solid #ccc;
    border-radius: 2px;
    padding: .5rem;
    margin-bottom: 1rem;
  }
</style>