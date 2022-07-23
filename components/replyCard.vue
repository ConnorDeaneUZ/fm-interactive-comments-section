<template>
  <section class="reply">
    <div class="reply-left">rating</div>

    <div class="reply-right">
      <div class="reply-right-upper">

      <form v-if="isUser">
        <a href="#" v-on:click="deleteReply(index, commentIndex)">DELETE</a>
      </form>
      
      <button @click="replyComment()">Reply</button>

      </div>
      <div class="reply-right-lower">
        {{reply}}
      </div>
    </div>

    <form v-if="isReplyActive">
      <input name="vitalInformation" v-model="replyInput" v-on:submit.prevent="submitForm">
      <a href="#" v-on:click="sendReplyComment(replyInput, index)">SUBMIT</a>
    </form>
  </section>
</template>

<script>
export default {
  name: 'reply',

  props: {
    reply: {
      Type: String,
      required: true
    },
    index: {
      Type: Number,
      required: true
    },
    commentIndex: {
      Type: Number,
      required: true
    }
  },

  data: () => ({
    isUser: true,
  }),

  methods: {
  
    deleteReply(index, commentIndex) {
      this.$emit('deleteReply', index, commentIndex)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '/assets/css/_color-palette';

.reply {
  display: flex;
  width: 720px;
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
</style>