<template>
  <div class="codeCreator">
    <div class="codeCreator__editors">
      <Editor :code="htmlCode" lang="html" @updateCode="newCode('htmlCode', $event)" />
      <Editor :code="cssCode" lang="css" @updateCode="newCode('cssCode', $event)" />
      <Editor :code="jsCode" lang="js" @updateCode="newCode('jsCode', $event)"/>
    </div>

    <div class="codeCreator__container">
      <iframe
        class="codeCreator__iframe"
        sandbox="allow-scripts"
        frameBorder="0"
        width="100%"
        ref="iframe"
      />
    </div>
  </div>
</template>

<script>
import html from "@/config/html.js"
import css from "@/config/css.js"
import js from "@/config/js.js"
import Editor from './components/Editor.vue'

export default {
  name: 'App',

  components: {
    Editor,
  },

  data() {
    return {
      htmlCode: html(),
      cssCode: css(),
      jsCode: js(),
    }
  },

  mounted(){
    this.processCode();
  },

  watch: {
    htmlCode() {
      this.processCode();
    },
    cssCode() {
      this.processCode();
    },
    jsCode() {
      this.processCode();
    },
  },

  methods: {
    processCode(){
      let html = document.createElement('html')
        html.innerHTML = `
          <body>
            ${this.htmlCode}
          </body>

          <style>
            ${this.cssCode}
          </style>
        `
      let script = document.createElement('script')
      script.innerHTML = this.jsCode || ""
      html.appendChild(script)
      this.$refs.iframe.srcdoc = html.outerHTML
    },

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
    position: relative;
    justify-content: space-around;
    height: 30vh;
    resize: vertical;
    overflow: auto;
  }

  &__container {
    height: 70vh;
  }

  &__iframe {
    display: block;
    height: 100%;
  }
}
</style>
