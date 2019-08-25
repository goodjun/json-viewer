<template>
  <div>
    <Tree :data="data" :empty-text="''"></Tree>
  </div>
</template>

<script>
export default {
  name: "tree-view",
  data() {
    return {
      data: []
    };
  },
  methods: {
    parseJson(obj) {
      let children = [];
      for (let key in obj) {
        if (typeof obj[key] === "object") {
          children.push({
            title: key,
            expand: false,
            children: this.parseChildren(obj[key])
          });
        } else {
          children.push({
            title: `${key}: "${obj[key]}"`,
            expand: false
          });
        }
      }
      this.data = [];
      this.data.push({
        title: "JSON",
        expand: true,
        children: children
      });
    },
    parseChildren(obj) {
      let children = [];
      for (let key in obj) {
        if (typeof obj[key] === "object") {
          children.push({
            title: key,
            expand: false,
            children: this.parseChildren(obj[key])
          });
        } else {
          children.push({
            title: `${key}: "${obj[key]}"`,
            expand: false
          });
        }
      }
      return children;
    }
  }
};
</script>

<style>
</style>
