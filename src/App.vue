<template>
  <h3>{{ info }}</h3>
  <p>{{ someInfo }}</p>

  <button type="button" @click="userData('Some new')">Send</button>
</template>

<script>
export default {
  data() {
    return {
      info: 'Title',
      someInfo: 'Anons of message',
    }
  },
  methods: {
    userData(word = 'New text') {
      // this.info = 'Some new'
      this.someInfo = word
    }
  }
}
</script>

<style scoped>
  h3 {
    font-weight: lighter;
  }

  p {
    color: rgb(203, 31, 31);
  }
</style>
