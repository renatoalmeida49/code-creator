<template>
<div class="editor">
  <codemirror
    class="editor__code"
    :style="style"
    v-model="rawCode"
    :extensions="extensions"
    @change="updateCode"
  />
</div>
</template>

<script>
import { Codemirror } from 'vue-codemirror'
import { javascript } from '@codemirror/lang-javascript'
import { html } from '@codemirror/lang-html'
import { css } from '@codemirror/lang-css'
import { oneDark } from '@codemirror/theme-one-dark'

const languages = {
  js: javascript(),
  html: html(),
  css: css(),
}

export default {
  name: "Editor",

  components: {
    Codemirror
  },

  props: {
    lang: { type: String, required: true },
    code: { type: String, required: true },
  },

  mounted() {
    this.rawCode = this.code
  },

  data() {
    return {
      rawCode: "",
      style: { height: '100%', width: '100%' }
    }
  },

  computed: {
    extensions() {
      return [languages[this.lang], oneDark]
    }
  },

  methods: {
    updateCode($event) {
      this.$emit('updateCode', $event)
    }
  }
}
</script>

<style lang="scss">
.editor {
  background: green;
  width: 100%;

  &__code {
    
    
  }
}
</style>