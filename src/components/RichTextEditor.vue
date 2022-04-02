<template>
  <div class="rich-text-menu-bar">
    <div class="item" ref="headRef">
      <el-select
        v-model="headLevel"
        class="m-2"
        placeholder="正文"
        size="small"
        style="width: 80px;"
        :disabled="headDisable"
        @change="commandHead"
      >
        <el-option
          v-for="item in headOptions"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        />
      </el-select>
    </div>
    <div class="item" ref="quoteRef">
      <button
        type="button"
        :class="{ disabled: quoteDisable }"
        :disabled="quoteDisable"
        @click="commandQuote"
      >
        <i class="fa fa-quote-left" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="strongRef">
      <button
        type="button"
        :class="{ disabled: strongDisable }"
        :disabled="strongDisable"
        @click="commandStrong"
      >
        <i class="fa fa-bold" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="fontFamilyRef">
      <el-select
        v-model="fontFamily"
        class="m-2"
        placeholder="默认字体"
        size="small"
        style="width: 80px;"
        :disabled="fontFamilyDisable"
        @change="commandfontFamily"
      >
        <el-option
          v-for="item in fontFamilyOptions"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        />
      </el-select>
    </div>
    <div class="item" ref="lineHeightRef">
      <el-select
        v-model="lineHeight"
        class="m-2"
        placeholder="默认行高"
        size="small"
        style="width: 80px;"
        :disabled="lineHeightDisable"
        @change="commandLineHeight"
      >
        <el-option
          v-for="item in lineHeightOptions"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        />
      </el-select>
    </div>
    <div class="item" ref="fontSizeRef">
      <el-select
        v-model="fontSize"
        class="m-2"
        placeholder="默认字号"
        size="small"
        style="width: 80px;"
        :disabled="fontSizeDisable"
        @change="commandfontSize"
      >
        <el-option
          v-for="item in fontSizeOptions"
          :key="item.value"
          :label="item.label"
          :value="item.value"
        />
      </el-select>
    </div>
    <div class="item" ref="orderListRef">
      <button
        type="button"
        :class="{ disabled: orderListDisable }"
        :disabled="orderListDisable"
        @click="commandOrderList"
      >
        <i class="fa fa-list-ol" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="unOrderListRef">
      <button
        type="button"
        :class="{ disabled: unOrderListDisable }"
        :disabled="unOrderListDisable"
        @click="commandUnOrderList"
      >
        <i class="fa fa-list-ul" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="clearRef">
      <button
        type="button"
        :class="{ disabled: clearDisable }"
        :disabled="clearDisable"
        @click="commandClear"
      >
        <i class="fa fa-eraser" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="underLineRef">
      <button
        type="button"
        :class="{ disabled: underLineDisable }"
        :disabled="underLineDisable"
        @click="commandUnderLine"
      >
        <i class="fa fa-underline" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="colorRef">
      <input
        type="color"
        style="position: absolute; visibility: hidden;"
        ref="colorPickerRef"
        @change="commandColor"
      />
      <button
        type="button"
        :class="{ disabled: colorDisable }"
        :disabled="colorDisable"
        @click="toggleColorPicker"
      >
        <i class="fa fa-font" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="delRef">
      <button
        type="button"
        :class="{ disabled: delDisable }"
        :disabled="delDisable"
        @click="commandDel"
      >
        <i class="fa fa-strikethrough" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="emRef">
      <button
        type="button"
        :class="{ disabled: emDisable }"
        :disabled="emDisable"
        @click="commandEm"
      >
        <i class="fa fa-italic" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="subRef">
      <button
        type="button"
        :class="{ disabled: subDisable }"
        :disabled="subDisable"
        @click="commandSub"
      >
        <i class="fa fa-subscript" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="supRef">
      <button
        type="button"
        :class="{ disabled: supDisable }"
        :disabled="supDisable"
        @click="commandSup"
      >
        <i class="fa fa-superscript" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="leftAlignRef">
      <button
        type="button"
        :class="{ disabled: leftAlignDisable }"
        :disabled="leftAlignDisable"
        @click="commandLeftAlign"
      >
        <i class="fa fa-align-left" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="centerAlignRef">
      <button
        type="button"
        :class="{ disabled: centerAlignDisable }"
        :disabled="centerAlignDisable"
        @click="commandCenterAlign"
      >
        <i class="fa fa-align-center" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="rightAlignRef">
      <button
        type="button"
        :class="{ disabled: rightAlignDisable }"
        :disabled="rightAlignDisable"
        @click="commandRightAlign"
      >
        <i class="fa fa-align-right" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="divideRef">
      <button
        type="button"
        :class="{ disabled: divideDisable }"
        :disabled="divideDisable"
        @click="commandDivide"
      >
        <i class="fa fa-bars" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item-divider"></div>
    <div class="item" ref="undoItemRef">
      <button
        type="button"
        :class="{ disabled: undoDisable }"
        :disabled="undoDisable"
        @click="commandUndo"
      >
        <i class="fa fa-undo" aria-hidden="true"></i>
      </button>
    </div>
    <div class="item" ref="redoItemRef">
      <button
        type="button"
        :class="{ disabled: redoDisable }"
        :disabled="redoDisable"
        @click="commandRedo"
      >
        <i class="fa fa-repeat" aria-hidden="true"></i>
      </button>
    </div>
  </div>
  <div class="rich-text-container" ref="richTextRef"></div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import { schema } from "prosemirror-schema-basic";
import { EditorState, Transaction } from "prosemirror-state";
import { EditorView } from "prosemirror-view";
import { undo, redo, history } from "prosemirror-history";
import { keymap } from "prosemirror-keymap";
import { baseKeymap, setBlockType, toggleMark, wrapIn } from "prosemirror-commands";
import { addListNodes, splitListItem, wrapInList } from "prosemirror-schema-list";
import { Schema, Node, NodeType } from "prosemirror-model";
import tippy from "tippy.js";

export default defineComponent({
  props: {
    doc: Object
  },

  setup(prop, { emit }) {
    const headRef = ref(null);
    const headDisable = ref(false);
    const headLevel = ref('');

    const quoteRef = ref(null);
    const quoteDisable = ref(false);

    const strongRef = ref(null);
    const strongDisable = ref(false);

    const fontFamilyRef = ref(null);
    const fontFamilyDisable = ref(false);
    const fontFamily = ref('');

    const lineHeightRef = ref(null);
    const lineHeightDisable = ref(false);
    const lineHeight = ref('');

    const fontSizeRef = ref(null);
    const fontSizeDisable = ref(false);
    const fontSize = ref('');

    const orderListRef = ref(null);
    const orderListDisable = ref(false);

    const unOrderListRef = ref(null);
    const unOrderListDisable = ref(false);

    const clearRef = ref(null);
    const clearDisable = ref(false);

    const underLineRef = ref(null);
    const underLineDisable = ref(false);

    const colorRef = ref(null);
    const colorDisable = ref(false);
    const colorPickerRef = ref(null);

    const delRef = ref(null);
    const delDisable = ref(false);

    const emRef = ref(null);
    const emDisable = ref(false);

    const subRef = ref(null);
    const subDisable = ref(false);

    const supRef = ref(null);
    const supDisable = ref(false);

    const leftAlignRef = ref(null);
    const leftAlignDisable = ref(false);

    const centerAlignRef = ref(null);
    const centerAlignDisable = ref(false);

    const rightAlignRef = ref(null);
    const rightAlignDisable = ref(false);

    const divideRef = ref(null);
    const divideDisable = ref(false);

    const undoItemRef = ref(null);
    const undoDisable = ref(false);

    const redoItemRef = ref(null);
    const redoDisable = ref(false);

    const richTextRef = ref(null);

    let editorView: EditorView;
    let mySchema: Schema;

    const headOptions = [
      {
        label: 'H1',
        value: 1
      },
      {
        label: 'H2',
        value: 2
      },
      {
        label: 'H3',
        value: 3
      },
      {
        label: 'H4',
        value: 4
      },
      {
        label: 'H5',
        value: 5
      },
      {
        label: '正文',
        value: ''
      }
    ];

    const fontFamilyOptions = [
      {
        label: '宋体',
        value: 'SimSun'
      },
      {
        label: '仿宋',
        value: 'FangSong'
      },
      {
        label: '黑体',
        value: 'SimHei'
      },
      {
        label: '楷体',
        value: 'KaiTi'
      },
      {
        label: '雅黑',
        value: 'Microsoft YaHei'
      },
    ];

    const fontSizeOptions = [
      {
        label: '12px',
        value: '12px'
      },
      {
        label: '13px',
        value: '13px'
      },
      {
        label: '14px',
        value: '14px'
      },
      {
        label: '15px',
        value: '15px'
      },
      {
        label: '16px',
        value: '16px'
      },
      {
        label: '19px',
        value: '19px'
      },
      {
        label: '22px',
        value: '22px'
      },
      {
        label: '24px',
        value: '24px'
      },
      {
        label: '29px',
        value: '29px'
      },
      {
        label: '32px',
        value: '32px'
      },
      {
        label: '40px',
        value: '40px'
      },
      {
        label: '48px',
        value: '48px'
      },
    ];

    const lineHeightOptions = [
      {
        label: '1',
        value: '1'
      },
      {
        label: '1.15',
        value: '1.15'
      },
      {
        label: '1.5',
        value: '1.5'
      },
      {
        label: '2',
        value: '2'
      },
      {
        label: '2.5',
        value: '2.5'
      },
      {
        label: '3',
        value: '3'
      },
    ];

    onMounted(() => {
      mySchema = new Schema({
        nodes: addListNodes((schema.spec.nodes as any).update('paragraph', {
          attrs: {
            textAlign: { default: 'left' },
            lineHeight: { default: 1 }
          },
          content: "inline*",
          group: "block",
          parseDOM: [{ tag: "p" }],
          toDOM: (node: any) => { return ['p', { style: `text-align: ${node.attrs.textAlign}; line-height: ${node.attrs.lineHeight}` }, 0] }
        }), "paragraph block*", "block"),
        marks: (schema.spec.marks as any).append({
          fontFamily: {
            attrs: {
              fontFamily: { default: 'Courier New' }
            },
            toDOM: (mark: any) => {
              return ['span', { style: `font-family: ${mark.attrs.fontFamily}` }];
            },
            parseDOM: [{ tag: 'span', style: 'font-family', getAttrs: (value: any) => value }]
          },
          fontSize: {
            attrs: {
              fontSize: { default: '16px' }
            },
            toDOM: (mark: any) => {
              return ['span', { style: `font-size: ${mark.attrs.fontSize}` }];
            },
            parseDOM: [{ tag: 'span', style: 'font-size', getAttrs: (value: any) => value }]
          },
          underLine: {
            toDOM: () => {
              return ['u', 0];
            },
            parseDOM: [{ tag: 'u' }]
          },
          color: {
            attrs: {
              color: { default: 'black' }
            },
            toDOM: (mark: any) => {
              return ['span', { style: `color: ${mark.attrs.color}` }];
            },
            parseDOM: [{ tag: 'span', style: 'color', getAttrs: (value: any) => value }]
          },
          strike: {
            toDOM: () => {
              return ['s', 0];
            },
            parseDOM: [{ tag: 's' }]
          },
          sub: {
            toDOM: () => {
              return ['sub', 0];
            },
            parseDOM: [{ tag: 'sub' }]
          },
          sup: {
            toDOM: () => {
              return ['sup', 0];
            },
            parseDOM: [{ tag: 'sup' }]
          }
        }),
      });

      const canApplyAlignCommand = (state: EditorState): boolean => {
        let { from, to } = state.selection;
        let applicable = false;
        state.doc.nodesBetween(from, to, (node) => {
          if (node.type == mySchema.nodes.paragraph) {
            applicable = true;
          } else {
            applicable = false;
          }
        })
        if (!applicable) return false;
        return true;
      }

      const canInsert = (state: EditorState, nodeType: NodeType) => {
        let $from = state.selection.$from
        for (let d = $from.depth; d >= 0; d--) {
          let index = $from.index(d)
          if ($from.node(d).canReplaceWith(index, index, nodeType)) return true
        }
        return false
      }

      const editorState = EditorState.create({
        schema: mySchema,
        doc: prop.doc ? Node.fromJSON(mySchema, prop.doc) : null,
        plugins: [
          history(),
          keymap({ "ctrl-z": undo, "ctrl-shift-z": redo, 'Enter': splitListItem(mySchema.nodes.list_item) }),
          keymap(baseKeymap),
        ],
      });
      editorView = new EditorView(richTextRef.value!, {
        state: editorState,
        dispatchTransaction: (transaction) => {
          let newState = editorView.state.apply(transaction);
          editorView.updateState(newState);

          emit('edit', editorView.state.doc.toJSON());

          headDisable.value = !setBlockType(mySchema.nodes.heading)(editorView.state);
          quoteDisable.value = !wrapIn(mySchema.nodes.blockquote)(editorView.state);
          strongDisable.value = !toggleMark(schema.marks.strong)(
            editorView.state
          );
          fontFamilyDisable.value = !toggleMark(mySchema.marks.fontFamily)(editorView.state);
          fontSizeDisable.value = !toggleMark(mySchema.marks.fontSize)(editorView.state);
          orderListDisable.value = !wrapInList(mySchema.nodes.ordered_list)(editorView.state);
          unOrderListDisable.value = !wrapInList(mySchema.nodes.bullet_list)(editorView.state);
          underLineDisable.value = !toggleMark(mySchema.marks.underLine)(editorView.state);
          colorDisable.value = !toggleMark(mySchema.marks.color)(editorView.state);
          delDisable.value = !toggleMark(mySchema.marks.strike)(editorView.state);
          emDisable.value = !toggleMark(mySchema.marks.em)(editorView.state);
          subDisable.value = !toggleMark(mySchema.marks.sub)(editorView.state);
          supDisable.value = !toggleMark(mySchema.marks.sup)(editorView.state);
          leftAlignDisable.value = !canApplyAlignCommand(editorView.state);
          centerAlignDisable.value = !canApplyAlignCommand(editorView.state);
          rightAlignDisable.value = !canApplyAlignCommand(editorView.state);
          divideDisable.value = !canInsert(editorView.state, mySchema.nodes.horizontal_rule);

          undoDisable.value = !undo(editorView.state);
          redoDisable.value = !redo(editorView.state);
        },
      });

      tippy(headRef.value!, {
        content: '标题'
      });
      tippy(quoteRef.value!, {
        content: '引用'
      });
      tippy(strongRef.value!, {
        content: "粗体",
      });
      tippy(fontFamilyRef.value!, {
        content: '字体'
      });
      tippy(lineHeightRef.value!, {
        content: '行高'
      });
      tippy(fontSizeRef.value!, {
        content: '字号'
      });
      tippy(orderListRef.value!, {
        content: '有序列表'
      });
      tippy(unOrderListRef.value!, {
        content: '无序列表'
      });
      tippy(clearRef.value!, {
        content: '清除格式'
      });
      tippy(underLineRef.value!, {
        content: '下划线'
      });
      tippy(colorRef.value!, {
        content: '文字颜色'
      });
      tippy(delRef.value!, {
        content: '删除线'
      });
      tippy(emRef.value!, {
        content: '斜体'
      });
      tippy(subRef.value!, {
        content: '下角标'
      });
      tippy(supRef.value!, {
        content: '上角标'
      });
      tippy(leftAlignRef.value!, {
        content: '左对齐'
      });
      tippy(centerAlignRef.value!, {
        content: '居中对齐'
      });
      tippy(rightAlignRef.value!, {
        content: '右对齐'
      });
      tippy(divideRef.value!, {
        content: '分割线'
      });
      tippy(undoItemRef.value!, {
        content: "撤销",
      });
      tippy(redoItemRef.value!, {
        content: "重做",
      });
    });

    // eslint-disable-next-line no-unused-vars
    const clearAllMarks = (state: EditorState, dispatch?: (tr: Transaction<any>) => void): boolean => {
      let { from, to } = state.selection;
      let applicable = true;
      if (!applicable) return false;
      if (dispatch) {
        dispatch(state.tr.removeMark(from, to));
      }
      return true;
    }

    const commandHead = (value: string) => {
      headLevel.value = value;
      if (value) {
        setBlockType(mySchema.nodes.heading, { level: value })(editorView.state, editorView.dispatch);
      } else {
        setBlockType(mySchema.nodes.paragraph)(editorView.state, editorView.dispatch);
      }
      editorView.focus();
    }

    const commandQuote = () => {
      wrapIn(mySchema.nodes.blockquote)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandStrong = () => {
      toggleMark(schema.marks.strong)(editorView.state, editorView.dispatch);
      editorView.focus();
    };

    const commandfontFamily = (value: string) => {
      fontFamily.value = value;
      toggleMark(mySchema.marks.fontFamily, { fontFamily: value })(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandLineHeight = (value: string) => {
      lineHeight.value = value;
      setBlockType(mySchema.nodes.paragraph, { lineHeight: value })(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandfontSize = (value: string) => {
      fontSize.value = value;
      toggleMark(mySchema.marks.fontSize, { fontSize: value })(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandOrderList = () => {
      wrapInList(mySchema.nodes.ordered_list)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandUnOrderList = () => {
      wrapInList(mySchema.nodes.bullet_list)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandClear = () => {
      clearAllMarks(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandUnderLine = () => {
      toggleMark(mySchema.marks.underLine)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandColor = (event: Event) => {
      toggleMark(mySchema.marks.color, { color: (event.target as HTMLInputElement).value })(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const toggleColorPicker = () => {
      (colorPickerRef.value as unknown as HTMLInputElement).click();
    }

    const commandDel = () => {
      toggleMark(mySchema.marks.strike)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandEm = () => {
      toggleMark(mySchema.marks.em)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandSub = () => {
      toggleMark(mySchema.marks.sub)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandSup = () => {
      toggleMark(mySchema.marks.sup)(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandLeftAlign = () => {
      setBlockType(mySchema.nodes.paragraph, { textAlign: 'left' })(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandCenterAlign = () => {
      setBlockType(mySchema.nodes.paragraph, { textAlign: 'center' })(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandRightAlign = () => {
      setBlockType(mySchema.nodes.paragraph, { textAlign: 'right' })(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    const commandDivide = () => {
      editorView.dispatch(editorView.state.tr.replaceSelectionWith(mySchema.nodes.horizontal_rule.create()));
      editorView.focus();
    }

    const commandUndo = () => {
      undo(editorView.state, editorView.dispatch);
      editorView.focus();
    };

    const commandRedo = () => {
      redo(editorView.state, editorView.dispatch);
      editorView.focus();
    }

    return {
      richTextRef,
      headRef,
      headDisable,
      headLevel,
      headOptions,
      quoteRef,
      quoteDisable,
      strongRef,
      strongDisable,
      fontFamilyRef,
      fontFamilyDisable,
      fontFamilyOptions,
      fontFamily,
      lineHeightRef,
      lineHeightDisable,
      lineHeight,
      lineHeightOptions,
      fontSizeRef,
      fontSizeDisable,
      fontSize,
      fontSizeOptions,
      orderListRef,
      orderListDisable,
      unOrderListRef,
      unOrderListDisable,
      clearRef,
      clearDisable,
      underLineRef,
      underLineDisable,
      colorRef,
      colorDisable,
      colorPickerRef,
      delRef,
      delDisable,
      emRef,
      emDisable,
      subRef,
      subDisable,
      supRef,
      supDisable,
      leftAlignRef,
      leftAlignDisable,
      centerAlignRef,
      centerAlignDisable,
      rightAlignRef,
      rightAlignDisable,
      divideRef,
      divideDisable,
      undoItemRef,
      undoDisable,
      redoItemRef,
      redoDisable,
      commandHead,
      commandQuote,
      commandStrong,
      commandfontFamily,
      commandLineHeight,
      commandfontSize,
      commandOrderList,
      commandUnOrderList,
      commandClear,
      commandUnderLine,
      commandColor,
      toggleColorPicker,
      commandDel,
      commandEm,
      commandSub,
      commandSup,
      commandLeftAlign,
      commandCenterAlign,
      commandRightAlign,
      commandDivide,
      commandUndo,
      commandRedo
    };
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
    position: relative;

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
