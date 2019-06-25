<template>
  <div>
    <ul>
      <li>
        <input type="radio" id="showdown" value="showdown" v-model="use_lib">
        <label for="showdown">Showdown</label>
      </li>
      <li>
        <input type="radio" id="markdown-it" value="markdown-it" v-model="use_lib">
        <label for="markdown-it">markdown-it</label>
      </li>
    </ul>
    <textarea rows="20" v-model="markdown"></textarea>
    <div v-html="html"></div>
  </div>
</template>

<script>
import showdown from 'showdown'
import MarkdownIt from 'markdown-it'
const converter = new showdown.Converter()
const md = new MarkdownIt()

const showdownConverter = (markdown) => {
  return converter.makeHtml(markdown)
}

const markdownItConverter = (markdown) => {
  return md.render(markdown)
}

export default {
  name: 'HelloWorld',
  data() {
    return {
      markdown: '',
      use_lib: 'showdown'
    }
  },
  computed: {
    html() {
      const converter = this.use_lib === 'showdown' ? showdownConverter : markdownItConverter
      console.log(`use_lib: ${this.use_lib}`)
      console.time('converter.makeHtml')
      const html = converter(this.markdown)
      console.timeEnd('converter.makeHtml')
      return html
    }
  }
}
</script>

<style scoped>
textarea {
  width: 100%;
}
</style>
