<template>
  <div id="app">
    <div><QiitaAPI /></div>
    <div><Firebase /></div>
    <div><ExampleApp /></div>
  </div>
</template>

<script>
import QiitaAPI from "@/components/QiitaAPI.vue"
import Firebase from "@/components/Firebase.vue"
import ExampleApp from "@/components/ExampleApp.vue"
export default {
  name: "App",
  components: {
    QiitaAPI,
    Firebase,
    ExampleApp,
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
