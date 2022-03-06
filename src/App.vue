<template>
  <div id="rich-text">
    <RichTextEditor />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import RichTextEditor from "./components/RichTextEditor.vue";

@Options({
  components: {
    RichTextEditor,
  },
})
export default class App extends Vue {}
</script>

<style scoped lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#rich-text {
  height: 800px;
}
</style>
