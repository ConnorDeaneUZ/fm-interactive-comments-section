<template>
  <section class="container">

    <div class="comments-container">
    <div class="comment-card" v-for="(comment, index) in comments" :key="index">

      <comment-card
      @deleteComment="deleteComment"
      :comment="comment.content"
      :index="index"
      :replies="comment.replies"
      />

    </div>

    <profile-card
    @postComment="postComment" />

      <!-- <form>
        <input name="vitalInformation" v-model="input" v-on:submit.prevent="submitForm">
        <a href="#" v-on:click="postComment(input)">SUBMIT</a>
      </form> -->

    </div>


  </section>
</template>

<script>
import commentCard from '../components/commentCard.vue'
import ProfileCard from '../components/profileCard.vue'
import replyCard from '../components/replyCard.vue'
import comments from '/config/data.json'

export default {
  name: 'IndexPage',

  components: {
    commentCard,
    replyCard,
    ProfileCard
  },

  data: () => ({
    comments: comments.comments,
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