<template>
  <div>
    <h1>Firestoreを使う</h1>
    <div>
      <button v-on:click="postMessage">メッセージをFirestoreに保存する</button>
      <div v-for="(message, index) in messages" v-bind:key="index">
        {{ message }}
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase"

export default {
  data() {
    return {
      messages: [],
    }
  },
  methods: {
    postMessage() {
      const data = { text: "こんにちは、メッセージの本文です。" }
      firebase
        .firestore()
        .collection("messages")
        .add(data)
        .then(() => {
          this.messages.push(data)
        })
    },
  },
  created() {
    firebase
      .firestore()
      .collection("messages")
      .get()
      .then((snapshot) => {
        for (let i = 0; i < snapshot.docs.length; i++) {
          this.messages.push(snapshot.docs[i].data())
        }
      })
  },
}
</script>
