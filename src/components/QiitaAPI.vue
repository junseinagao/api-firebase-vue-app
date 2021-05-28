<template>
  <div>
    <h1>Qiita APIを使う</h1>
    <div>
      <h2>Qiitaの記事</h2>
      <button v-on:click="getQiitaArticle">記事を取得する</button>
      <div v-for="(article, index) in articles" v-bind:key="index">
        {{ index }} : {{ article }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      articles: [],
      user: {},
    }
  },
  methods: {
    getQiitaArticle: function () {
      fetch(`https://qiita.com/api/v2/items`)
        .then((res) => {
          return res.json()
        })
        .then((value) => {
          this.articles = value
        })
        .catch((error) => {
          console.error(error)
        })
    },
  },
}
</script>
