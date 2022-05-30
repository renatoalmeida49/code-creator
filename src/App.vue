<template>
  <div class="codeCreator">
    <div class="codeCreator__editors">
      <Editor />
      <Editor />
      <Editor />
    </div>

    <div>
      <h1>Iframe</h1>
    </div>
  </div>
</template>

<script>
import Editor from './components/Editor.vue'

export default {
  name: 'App',

  components: {
    Editor,
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
  text-align: center;
  color: #2c3e50;
}

.codeCreator {
  &__editors {
    background: red;
    display: flex;
    justify-content: space-between;
  }
}
</style>
