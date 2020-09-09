<template lang="pug">
  #app
    show-blogs

</template>

<script>
import showBlogs from './components/showBlogs.vue'

export default {
  name: 'App',
  components: {
    'show-blogs': showBlogs
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
