<template>
  <section class="profile">
    <img src="" alt="">
    <form>
      <input name="profile-form" v-model="input" v-on:submit.prevent="submitForm">
      <a href="#" v-on:click="postComment(input)">SUBMIT</a>
    </form>
  </section>
</template>

<script>
export default {
  name: 'profile',

  data: () => ({
    input: '',
  }),

  methods: {
    postComment(input) {
      this.$emit('postComment', input)
    }
  }
}
</script>

<style lang="scss" scoped>
@import '/assets/css/_color-palette';

.profile {
  margin: 20px;
  width: 815px;
  height: 160px;
  background-color: colorPaletteSetting(core-white);
}
</style>