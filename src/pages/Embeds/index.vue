<template>
  <q-page padding class="editor">
    <editor-content class="editor__content" :editor="editor" />
  </q-page>
</template>

<script>
import { UiMixin, PageMixin } from 'src/mixins'
import { Editor, EditorContent } from 'tiptap'
import {
  HardBreak,
  Heading,
  Bold,
  Italic,
  History
} from 'tiptap-extensions'
import Iframe from './Iframe.js'

export default {
  mixins: [ UiMixin, PageMixin ],
  components: {
    EditorContent
  },
  data () {
    return {
      editor: new Editor({
        extensions: [
          new HardBreak(),
          new Heading({ levels: [1, 2, 3] }),
          new Bold(),
          new Italic(),
          new History(),
          // custom extension
          new Iframe()
        ],
        content: `
          <h2>
            Embeds
          </h2>
          <p>
            This is an example of a custom iframe node. This iframe is rendered as a <strong>vue component</strong>. This makes it possible to render the input below to change its source.
          </p>
          <iframe src="https://www.youtube.com/embed/XIMLoLxmTDw" frameborder="0" allowfullscreen></iframe>
        `
      })
    }
  },
  beforeDestroy () {
    this.editor.destroy()
  }
}
</script>

<style lang="scss">
@import "src/css/variables";

.iframe {
  &__embed {
    width: 100%;
    height: 15rem;
    border: 0;
  }

  &__input {
    display: block;
    width: 100%;
    font: inherit;
    border: 0;
    border-radius: 5px;
    background-color: rgba($color-black, 0.1);
    padding: 0.3rem 0.5rem;
  }
}
</style>
