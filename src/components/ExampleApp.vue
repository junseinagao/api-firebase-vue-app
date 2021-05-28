<template>
  <div>
    <h1>Qiita APIとFirestoreを使った実践的なアプリ</h1>
    <div>
      <button v-on:click="getQiitaArticleTitles">記事を取得する</button>
      <div>取得するページ<input type="number" v-model="page" /></div>
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
      page: 1,
    }
  },
  methods: {
    getQiitaArticleTitles: function () {
      if (this.page > 0) {
        fetch(
          `https://qiita.com/api/v2/items?page=${this.page}&per_page=10&query=tag:Vue.js`
        )
          .then((res) => {
            return res.json()
          })
          .then((data) => {
            for (let i = 0; i < data.length; i++) {
              this.articles.push(data[i])
              firebase.firestore().collection("articles").add(data[i])
            }
          })
      }
    },
  },
  created() {
    firebase
      .firestore()
      .collection("articles")
      .get()
      .then((snapshot) => {
        return snapshot.docs
      })
      .then((docs) => {
        for (let i = 0; i < docs.length; i++) {
          this.articles.push(docs[i].data())
        }
      })
  },
}
</script>
