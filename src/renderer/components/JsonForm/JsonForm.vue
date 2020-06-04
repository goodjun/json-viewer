<template>
  <div class="json-form-warp">
    <Button icon="ios-code" @click="formatJson()">Format</Button>
    <!-- <Button icon="ios-redo-outline" @click="exportExcel()">Export</Button> -->
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
  mounted() {
    window.addEventListener("resize", e => {
      this.editorHeight = window.innerHeight - 150;
      e.preventDefault();
    });
  },
  created() {
    //
  },
  methods: {
    editorInit() {
      require("brace/mode/javascript");
      require("brace/theme/chrome");
    },
    formatJson(save = true) {
      try {
        const obj = JSON.parse(this.$refs.editor.session.getValue());
        if (typeof obj === "object") {
          const json = JSON.stringify(obj, null, 2);
          this.$refs.editor.session.setValue(json);
          if (this.lastJson !== json) {
            this.$emit("parseJson", obj);
            if (save) this.$emit("saveJson", obj);
          }
          this.lastJson = json;
        } else {
          this.$Message.error("This is not JSON");
          return;
        }
      } catch (e) {
        this.$Message.error("This is not JSON");
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
  }
};
</script>

<style>
.json-form-warp {
  margin-right: 10px;
}
</style>
