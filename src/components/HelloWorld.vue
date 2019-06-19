<template>
  <div>
    <textarea rows="20" v-model="markdown"></textarea>
    <div v-html="html"></div>
  </div>
</template>

<script>
import showdown from 'showdown'
const converter = new showdown.Converter()

export default {
  name: 'HelloWorld',
  data() {
    return {
      markdown: ''
    }
  },
  computed: {
    html() {
      return converter.makeHtml(this.markdown)
    }
  }
}
</script>

<style scoped>
textarea {
  width: 100%;
}
</style>
