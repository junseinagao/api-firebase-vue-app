<template>
  <div id="app"><GithubAPI /></div>
</template>

<script>
import GithubAPI from "@/components/GithubAPI.vue"
export default {
  name: "App",
  components: {
    GithubAPI,
  },
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
