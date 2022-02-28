<template>
  <div class="rich-text-container" ref="richText"></div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import { schema } from "prosemirror-schema-basic";
import { EditorState } from "prosemirror-state";
import { EditorView } from "prosemirror-view";
import { undo, redo, history } from "prosemirror-history";
import { keymap } from "prosemirror-keymap";
import { baseKeymap } from "prosemirror-commands";
import { menuBar } from "prosemirror-menu";
import { buildMenuItems } from "prosemirror-example-setup";

@Options({
  props: {
    msg: String,
  },
})
export default class RichTextEditor extends Vue {
  mounted() {
    const state = EditorState.create({
      schema,
      plugins: [
        history(),
        keymap({ "ctrl-z": undo, "ctrl-shift-z": redo }),
        keymap(baseKeymap),
        menuBar({ floating: false, content: buildMenuItems(schema).fullMenu }),
      ],
    });
    const view = new EditorView(this.$refs.richText as Node, {
      state,
      dispatchTransaction(transaction) {
        console.log(
          "Document size went from",
          transaction.before.content.size,
          "to",
          transaction.doc.content.size
        );
        let newState = view.state.apply(transaction);
        view.updateState(newState);
      },
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
@import 'prosemirror-menu/style/menu.css';
@import 'prosemirror-view/style/prosemirror.css';
@import 'prosemirror-example-setup/style/style.css';

.rich-text-container {
  border: 1px solid black;
  height: 100%;

  .ProseMirror-example-setup-style hr {
    padding: 2px 10px;
    border: none;
    margin: 1em 0;
  }

  .ProseMirror-example-setup-style hr:after {
    content: "";
    display: block;
    height: 1px;
    background-color: silver;
    line-height: 2px;
  }

  .ProseMirror ul,
  .ProseMirror ol {
    padding-left: 30px;
  }

  .ProseMirror blockquote {
    padding-left: 1em;
    border-left: 3px solid #eee;
    margin-left: 0;
    margin-right: 0;
  }

  .ProseMirror-example-setup-style img {
    cursor: default;
  }

  .ProseMirror-prompt {
    background: white;
    padding: 5px 10px 5px 15px;
    border: 1px solid silver;
    position: fixed;
    border-radius: 3px;
    z-index: 11;
    box-shadow: -0.5px 2px 5px rgba(0, 0, 0, 0.2);
  }

  .ProseMirror-prompt h5 {
    margin: 0;
    font-weight: normal;
    font-size: 100%;
    color: #444;
  }

  .ProseMirror-prompt input[type="text"],
  .ProseMirror-prompt textarea {
    background: #eee;
    border: none;
    outline: none;
  }

  .ProseMirror-prompt input[type="text"] {
    padding: 0 4px;
  }

  .ProseMirror-prompt-close {
    position: absolute;
    left: 2px;
    top: 1px;
    color: #666;
    border: none;
    background: transparent;
    padding: 0;
  }

  .ProseMirror-prompt-close:after {
    content: "✕";
    font-size: 12px;
  }

  .ProseMirror-invalid {
    background: #ffc;
    border: 1px solid #cc7;
    border-radius: 4px;
    padding: 5px 10px;
    position: absolute;
    min-width: 10em;
  }

  .ProseMirror-prompt-buttons {
    margin-top: 5px;
    display: none;
  }
}
</style>
