<template>
  <div class="codeCreator">
    <div class="codeCreator__editors">
      <Editor :code="htmlCode" lang="html" @updateCode="newCode('htmlCode', $event)" />
      <Editor :code="cssCode" lang="css" @updateCode="newCode('cssCode', $event)" />
      <Editor :code="jsCode" lang="js" @updateCode="newCode('jsCode', $event)"/>
    </div>

    <iframe
      :srcdoc="srcdoc"
      sandbox="allow-scripts"
      frameBorder="0"
      width="100%"
    />
  </div>
</template>

<script>
import Editor from './components/Editor.vue'

export default {
  name: 'App',

  components: {
    Editor,
  },

  data() {
    return {
      htmlCode: "",
      cssCode: "h1 { background: red }",
      jsCode: ""
    }
  },

  computed: {
    srcdoc() {
      return `
        <html>
          <body>
            ${this.htmlCode}
          </body>

          <style>
            ${this.cssCode}
          </style>

          
        </html>
      `
    },
  },

  methods: {
    newCode(key, $event) {
      this[key] = $event
    }
  }
}
</script>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.codeCreator {
  min-height: 100vh;

  &__editors {
    display: flex;
    justify-content: space-around;
  }
}
</style>
