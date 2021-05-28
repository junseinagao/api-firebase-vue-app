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
      firebase
        .firestore()
        .collection("messages")
        .add({
          text: "こんにちは、メッセージの本文です。",
        })
        .then((doc) => {
          firebase.firestore().collection("messages").doc(doc.id).set(
            {
              id: doc.id,
            },
            { merge: true }
          )
          this.messages.push({
            id: doc.id,
            text: "こんにちは、メッセージの本文です。",
          })
        })
    },
  },
  created() {
    firebase
      .firestore()
      .collection("messages")
      .get()
      .then((snapshot) => {
        snapshot.docs.forEach((doc) => {
          this.messages.push(doc.data())
        })
      })
  },
}
</script>
