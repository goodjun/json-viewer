<template>
  <codemirror v-model="code" :options="cmOptions" class="code"></codemirror>
</template>

<script>
import { codemirror } from "vue-codemirror";

// language js
// import "codemirror/mode/javascript/javascript.js";

// theme css
// import "codemirror/theme/blackboard.css";
// addon js css
// import "codemirror/addon/hint/show-hint.css";
// import "codemirror/addon/hint/show-hint.js";
// import "codemirror/addon/hint/javascript-hint.js";

//导入使用的语言语法定义文件
require("codemirror/mode/python/python.js");
require("codemirror/mode/javascript/javascript.js");
require("codemirror/mode/clike/clike.js");
require("codemirror/mode/shell/shell.js");
//导入选中的theme文件
require("codemirror/theme/blackboard.css");
//导入自动提示核心文件及样式
require("codemirror/addon/hint/show-hint.css");
require("codemirror/addon/hint/show-hint.js");
//导入指定语言的提示文件
require("codemirror/addon/hint/javascript-hint.js");

export default {
  name: "json-form",
  components: {
    codemirror
  },
  data() {
    return {
      code: "var a=1\nlet b=2",
      cmOptions: {
        tabSize: 4,
        mode: "text/javascript",
        theme: "blackboard",
        lineNumbers: true,
        line: true
      }
    };
  }
};
</script>

<style>
</style>
