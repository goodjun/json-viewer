<template>
  <div>
    <Button icon="ios-code">Format</Button>
    <Button icon="ios-redo-outline">Export</Button>
    <br />
    <br />
    <textarea ref="mycode" v-model="code"></textarea>
  </div>
</template>

<script>
import "codemirror/lib/codemirror.css";
import "codemirror/addon/hint/show-hint.css";

let CodeMirror = require("codemirror/lib/codemirror");

require("codemirror/mode/javascript/javascript");

require("codemirror/addon/edit/matchbrackets");
require("codemirror/addon/selection/active-line");
require("codemirror/addon/hint/show-hint");

export default {
  name: "json-form",
  data() {
    return {
      code: '{"name": "tom"}'
    };
  },
  created() {
    //
  },
  methods: {
    test() {
      //
    }
  },
  mounted() {
    window.addEventListener("resize", e => {
      console.log(window.innerHeight);
      e.preventDefault();
    });

    let editor = CodeMirror.fromTextArea(this.$refs.mycode, {
      mode: "text/javascript",
      indentWithTabs: true,
      smartIndent: true,
      lineNumbers: true,
      matchBrackets: true,
      autofocus: true,
      lineWrapping: true,
      indentUnit: 4
    });
  }
};
</script>

<style>
.CodeMirror {
  /* 146px */
  height: 400px;
}
</style>
