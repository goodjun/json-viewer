<template>
  <div class="tree-view-warp">
    <Tree
      :data="data"
      :empty-text="''"
      :style="{ height: height + 'px' }"
    ></Tree>
  </div>
</template>

<script>
export default {
  name: "tree-view",
  data() {
    return {
      data: [],
      height: window.innerHeight - 100,
    };
  },
  mounted() {
    window.addEventListener("resize", (e) => {
      this.height = window.innerHeight - 100;
      e.preventDefault();
    });
  },
  methods: {
    parseJson(obj) {
      let children = [];
      for (let key in obj) {
        if (typeof obj[key] === "object") {
          children.push({
            title: key,
            expand: false,
            children: this.parseChildren(obj[key]),
          });
        } else {
          children.push({
            title: `${key}: "${obj[key]}"`,
            expand: false,
          });
        }
      }
      this.data = [];
      this.data.push({
        title: "JSON",
        expand: true,
        children: children,
      });
    },
    parseChildren(obj) {
      let children = [];
      for (let key in obj) {
        if (typeof obj[key] === "object") {
          children.push({
            title: key,
            expand: false,
            children: this.parseChildren(obj[key]),
          });
        } else {
          children.push({
            title: `${key}: "${obj[key]}"`,
            expand: false,
          });
        }
      }
      return children;
    },
  },
};
</script>

<style>
.ivu-tree {
  overflow: overlay;
}
.tree-view-warp {
  margin-right: 10px;
}
</style>
