<template>
  <section class="container">

    <div class="comments-container">
    <div class="comment-card" v-for="(comment, index) in comments" :key="index">

      <comment-card
      @deleteComment="deleteComment"
      :comment="comment.content"
      :index="index"/>

      <div class="reply-card" v-for="(reply, index) in comment.replies" :key="index">
        <reply-card
        @deleteReply="deleteReply"
        :reply="reply.content"
        :index="index"
        :commentIndex="comment.index"/>

      </div>

      <!-- <pre>
        {{comment}}

      <form>
        <input name="vitalInformation" v-model="replyInput" v-on:submit.prevent="submitForm">
        <a href="#" v-on:click="replyComment(replyInput, index)">SUBMIT</a>
      </form>

      <form>
        <a href="#" v-on:click="deleteComment(index)">DELETE</a>
      </form>
      </pre> -->

      <!-- <form>
        <a href="#" @deleteComment="deleteComment">DELETE</a>
      </form> -->

    </div>

      <form>
        <input name="vitalInformation" v-model="input" v-on:submit.prevent="submitForm">
        <a href="#" v-on:click="postComment(input)">SUBMIT</a>
      </form>


    </div>


  </section>
</template>

<script>
import commentCard from '../components/commentCard.vue'
import replyCard from '../components/replyCard.vue'
import comments from '/config/data.json'

export default {
  name: 'IndexPage',

  components: {
    commentCard,
    replyCard
  },

  data: () => ({
    comments: comments.comments,
    input: '',
    replyInput:''
  }),

  methods: {
    postComment(input) {
      this.comments.push(input)
    },

    replyComment(input, index) {
      this.comments[index].replies.push(input)
    },

    deleteComment(index) {
      console.log('Index here', index)
      console.log("COMMENT INDEX", this.comments[index])
      this.comments.splice(index, 1)
    },

    deleteReply(index, commentIndex) {
      console.log('COMMENTS INDEX', commentIndex)
      console.log('Reply INDEX', index)
      this.comments[1].replies.splice(index, 1)
    }
  }
}
</script>

<style lang="scss">
@import '/assets/css/_color-palette';

body {
  margin: 0 !important;
  padding: 0 !important;
  box-sizing: border-box !important;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  height: 100vh;
  width: 100%;
  background-color: colorPaletteSetting(light-blue);
}

.comments-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.comment-card {
  display: flex;
  flex-direction: column;
  justify-content: flex-end ;
}

.reply-card {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}
</style>