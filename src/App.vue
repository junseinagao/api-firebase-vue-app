<template>
  <div id="app">
    <div><QiitaAPI /></div>
    <div><FirebaseApp /></div>
    <div><ExampleApp /></div>
  </div>
</template>

<script>
import QiitaAPI from "@/components/QiitaAPI.vue"
import FirebaseApp from "@/components/FirebaseApp.vue"
import ExampleApp from "@/components/ExampleApp.vue"
export default {
  name: "App",
  components: {
    QiitaAPI,
    FirebaseApp,
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
