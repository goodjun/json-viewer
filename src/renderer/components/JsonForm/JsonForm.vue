<template>
  <div>
    <Button icon="ios-code" @click="formatJson()">Format</Button>
    <Button icon="ios-redo-outline" @click="exportExcel()">Export</Button>
    <br />
    <br />
    <editor
      ref="editor"
      theme="chrome"
      :height="editorHeight"
      :content="code"
      :options="editorOptions"
      :fontSize="14"
      :lang="'javascript'"
      @onChange="editorChange"
      @init="editorInit"
    ></editor>
  </div>
</template>

<script>
import Editor from "../../../../node_modules/vue2x-ace-editor";

export default {
  name: "json-form",
  components: {
    Editor
  },
  data() {
    return {
      code: "",
      lastJson: "",
      editorOptions: {
        enableSnippets: false,
        tabSize: 2,
        enableBasicAutocompletion: false,
        enableLiveAutocompletion: false,
        useWrapMode: true,
        indentedSoftWrap: false,
        behavioursEnabled: false,
        wrap: "free"
      },
      editorHeightOffset: 150,
      editorHeight: window.innerHeight - 150
    };
  },
  created() {
    //
  },
  methods: {
    editorInit() {
      require("brace/mode/javascript");
      require("brace/theme/chrome");
    },
    editorChange() {
      //
    },
    formatJson(save = true) {
      try {
        const obj = JSON.parse(this.$refs.editor.session.getValue());
        if (typeof obj === "object") {
          const json = JSON.stringify(obj, null, 2);
          this.$refs.editor.session.setValue(json);
          if (save && this.lastJson !== json) this.$emit("onFormatJson", obj);
          this.lastJson = json;
        } else {
          this.$Message.error("This is not JSON");
          console.error("This is not JSON");
          return;
        }
      } catch (e) {
        this.$Message.error("This is not JSON");
        console.error("This is not JSON");
        return;
      }
    },
    exportExcel() {
      // TODO: 导出功能
    },
    onReadJson(json) {
      this.$refs.editor.session.setValue(json);
      this.formatJson(false);
    }
  },
  mounted() {
    window.addEventListener("resize", e => {
      this.editorHeight = window.innerHeight - 150;
      e.preventDefault();
    });
  }
};
</script>

<style>
</style>
