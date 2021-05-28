<template>
  <div>
    <button v-on:click="getCommitsUsingFetch">Get Commits</button>
    <div>合計Commit数:{{ results.length }}</div>
    <div v-for="(result, index) in results" v-bind:key="index">
      {{ index }} : {{ result.commit.message }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      results: [],
    }
  },
  methods: {
    getCommitsUsingFetch: function () {
      this.results = []
      fetch(
        `https://api.github.com/repos/Hikarutakakura/js-recipe/commits?per_page=100`
      )
        .then((res) => {
          return res.json()
        })
        .then((value) => {
          console.log(value)
          this.results.push(...value)
        })
        .catch((error) => {
          console.error(error)
        })
    },
  },
}
</script>
