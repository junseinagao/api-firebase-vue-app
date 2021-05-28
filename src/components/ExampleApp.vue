<template>
  <div>
    <h1>Qiita APIとFirestoreを使った実践的なアプリ</h1>
    <div>
      <button v-on:click="getQiitaArticleTitles">記事を取得する</button>
      <div v-for="(article, index) in articles" v-bind:key="index">
        {{ index }} : {{ article.title }}
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase"

export default {
  data() {
    return {
      articles: [],
    }
  },
  methods: {
    getQiitaArticleTitles: async function () {
      const result = await fetch(
        `https://qiita.com/api/v2/items?page=1&per_page=10&query=tag:Vue.js`
      ).then((res) => {
        return res.json()
      })
      for (let i = 0; i < result.length; i++) {
        this.articles.push(result[i])
        await firebase.firestore().collection("articles").add(result[i])
      }
    },
  },
  created() {
    firebase
      .firestore()
      .collection("articles")
      .get()
      .then((snapshot) => {
        snapshot.docs.forEach((doc) => {
          this.articles.push(doc.data())
        })
      })
  },
}
</script>
