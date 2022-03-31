<template>
  <div id="rich-text">
    <RichTextEditor :doc="doc" @edit="logoEditData" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import RichTextEditor from "./components/RichTextEditor.vue";

export default defineComponent({
  components: {
    RichTextEditor
  },
  data() {
    return {
      doc: undefined
    };
  },
  beforeMount() {
    const content = localStorage.getItem('content');
    this.doc = content ? JSON.parse(content) : undefined;
  },
  methods: {
    logoEditData(data: any) {
      localStorage.setItem('content', JSON.stringify(data));
    }
  }
});
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
