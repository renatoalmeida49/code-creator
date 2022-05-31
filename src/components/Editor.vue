<template>
<div class="editor">
  <h1 class="editor__title">{{ getTitle }}</h1>

  <div class="editor__container">
    <codemirror
      class="editor__code"
      :style="style"
      v-model="rawCode"
      :extensions="extensions"
      @change="updateCode"
    />
  </div>
</div>
</template>

<script>
import { Codemirror } from 'vue-codemirror'
import { javascript } from '@codemirror/lang-javascript'
import { html } from '@codemirror/lang-html'
import { css } from '@codemirror/lang-css'
import { oneDark } from '@codemirror/theme-one-dark'

const languages = {
  js: {
    code: javascript(),
    label: "JavaScript"
  },
  html: {
    code: html(),
    label: "HTML"
  },
  css: {
    code: css(),
    label: "CSS"
  }
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

  data() {
    return {
      rawCode: "",
      style: { height: "100%", width: '100%' }
    }
  },

  mounted() {
    this.rawCode = this.code
  },

  computed: {
    extensions() {
      return [languages[this.lang].code, oneDark]
    },

    getTitle() {
      return languages[this.lang].label
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
  background: #f1f1f1;
  width: 100%;
  padding: 20px;

  &__title {
    height: 37px
  }
  
  &__container {
    height: calc(100% - 37px);
  }
}
</style>