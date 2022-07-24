<template>
  <section class="comment-container">

    <div class="comment">
      <div class="comment-left">rating</div>

    <div class="comment-right">
      <div class="comment-right-upper">

      <form v-if="isUser">
        <a href="#" v-on:click="deleteComment(index)">DELETE</a>
      </form>
      
      <button @click="replyComment()">Reply</button>

      </div>
      <div class="comment-right-lower">
        {{comment}}
      </div>
    </div>

    <!-- <form v-if="isReplyActive">
      <input name="vitalInformation" v-model="replyInput" v-on:submit.prevent="submitForm">
      <a href="#" v-on:click="sendReplyComment(replyInput, index)">SUBMIT</a>
    </form> -->
    </div>

      <div class="reply">

      <div class="reply-card" v-for="(reply, index) in replies" :key="index">
        <reply-card
          @deleteReply="deleteReply"
          :reply="reply.content"
          :index="index"
          :commentIndex="comment.index"/>
        </div>
      </div>


  </section>
</template>

<script>
export default {
  name: 'comment',

  data: () => ({
    isReplyActive: false,
    isUser: true,
    replyInput: ''
  }),

  props: {
    comment: {
      type: String,
      required: true
    },
    index: {
      Type: Number,
      required: true
    },
    replies: {
      Type: Array,
      required: true
    }
  },

  methods: {

    sendReplyComment(input) {
      this.replies.push(input)
    },

    replyComment() {
      this.isReplyActive = !this.isReplyActive
    },

    deleteComment(index) {
      this.$emit('deleteComment', index)
    },

    deleteReply(index) {
      this.replies.splice(index, 1)
    }

  }

}
</script>

<style lang="scss" scoped>
@import '/assets/css/_color-palette';

.comment {
  display: flex;
  width: 815px;
  height: 190px;
  background-color: colorPaletteSetting(core-white);
  margin: 20px;

  &-right {
    // background-color: red;

    &-upper {
      display: flex;
      justify-content: flex-end;
      height: 80px;
      // background-color: green;
    }

    &-lower {
      padding: 10px;
    }
  }

  &-left {
    width: 100px;
    height: 100%;
    background-color: colorPaletteSetting(core-light-grey);
  }
}

.reply {
  position: relative;
  // background-color: firebrick;
}

.reply-card {
  &::before {
    position: absolute;
    content: '';
    left: 50px;
    width: 2px;
    height: 230px;
    background-color: colorPaletteSetting(core-light-grey);
  }
}
</style>