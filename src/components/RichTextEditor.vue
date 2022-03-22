<template>
  <div class="rich-text-menu-bar">
    <div class="item" ref="strong">
      <button
        type="button"
        :class="{ disabled: strongDisable }"
        :disabled="strongDisable"
        @click="commandStrong"
      >
        <i class="fa fa-bold" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item-divider"></div>
    <div class="item" ref="undoItem">
      <button
        type="button"
        :class="{ disabled: strongDisable }"
        :disabled="strongDisable"
        @click="commandStrong"
      >
        <i class="fa fa-undo" aria-hidden="true"></i>
      </button>
    </div>
  </div>
  <div class="rich-text-container" ref="richText"></div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import { schema } from "prosemirror-schema-basic";
import { EditorState } from "prosemirror-state";
import { EditorView } from "prosemirror-view";
import { undo, redo, history } from "prosemirror-history";
import { keymap } from "prosemirror-keymap";
import { baseKeymap, toggleMark } from "prosemirror-commands";
import { addListNodes } from "prosemirror-schema-list";
import { Schema } from "prosemirror-model";
import tippy from "tippy.js";

export default defineComponent({
  setup() {
    const strong = ref(null);
    const strongDisable = ref(false);

    const undoItem = ref(null);

    const richText = ref(null);

    let editorView: EditorView;

    onMounted(() => {
      const mySchema = new Schema({
        nodes: addListNodes(schema.spec.nodes, "paragraph block*", "block"),
        marks: schema.spec.marks,
      });
      const editorState = EditorState.create({
        schema: mySchema,
        plugins: [
          history(),
          keymap({ "ctrl-z": undo, "ctrl-shift-z": redo }),
          keymap(baseKeymap),
        ],
      });
      editorView = new EditorView(richText.value!, {
        state: editorState,
        dispatchTransaction: (transaction) => {
          let newState = editorView.state.apply(transaction);
          editorView.updateState(newState);

          strongDisable.value = toggleMark(schema.marks.strong)(
            editorView.state
          );
        },
      });

      tippy(strong.value!, {
        content: "粗体",
      });
      tippy(undoItem.value!, {
        content: '撤销'
      });
    });

    const commandStrong = () => {
      toggleMark(schema.marks.strong)(editorView.state, editorView.dispatch);
      editorView.focus();
    };

    return { strong, richText, strongDisable, undoItem, commandStrong };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
@import "prosemirror-view/style/prosemirror.css";
@import "tippy.js/dist/tippy.css";
@import "../assets/font-awesome-4.7.0/css/font-awesome.min.css";

.rich-text-menu-bar {
  display: flex;
  padding: 2px;
  border: 1px solid #ccc;

  .item {
    display: inline-flex;
    height: 36px;
    padding: 4px;
    box-sizing: border-box;
    min-width: 36px;
    justify-content: center;
    align-items: center;

    button {
      cursor: pointer;
      height: 100%;
      border: none;
      background-color: transparent;
      font-size: 16px;
      border-radius: 4px;

      &:hover {
        font-weight: bold;
        background-color: rgba(0, 0, 0, 0.2);
      }

      &.disabled {
        cursor: not-allowed;
      }
    }
  }

  .item-divider {
    width: 1px;
    background-color: #ccc;
  }
}

.rich-text-container {
  height: 100%;

  & p {
    margin: 0;
  }

  & .ProseMirror {
    border: 1px solid #ccc;
    box-sizing: border-box;
    height: 100%;
    padding: 2px;
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
