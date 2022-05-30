<template>
  <div class="codeCreator">
    <div class="codeCreator__editors">
      <Editor :code="htmlCode" lang="html" @updateCode="newCode('htmlCode', $event)" />
      <Editor :code="cssCode" lang="css" @updateCode="newCode('cssCode', $event)" />
      <Editor :code="jsCode" lang="js" @updateCode="newCode('jsCode', $event)"/>
    </div>

    <iframe
      sandbox="allow-scripts"
      frameBorder="0"
      width="100%"
      ref="iframe"
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
      htmlCode: "<h1>TEST</h1>",
      cssCode: "h1 { background: red }",
      jsCode: "console.log('bagaceira');",
      // test: "<html><title>TEST</title><body><h1>Hello World</h1></body><style>h1{ background: blue };</style></html>"
    }
  },
  mounted(){
    this.processCode();
  },
  watch: {
    htmlCode: function() {
      this.processCode();
    },
    cssCode: function() {
      this.processCode();
    },
    jsCode: function() {
      this.processCode();
    },
  },
  methods: {
    processCode(){
       let html = document.createElement('html')
        html.innerHTML = `
          <html>
            <body>
              ${this.htmlCode}
            </body>

            <style>
              ${this.cssCode}
            </style>
          
          </html>
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
    justify-content: space-around;
  }
}
</style>
