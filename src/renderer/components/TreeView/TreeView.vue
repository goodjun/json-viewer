<template>
  <div>
    <Tree :data="data"></Tree>
  </div>
</template>

<script>
export default {
  name: "tree-view",
  data() {
    return {
      data: [
        {
          title: "JSON",
          expand: true,
          children: [
            {
              title: 'tom: "tom"'
            }
          ]
        }
      ]
    };
  }
};
</script>

<style>
</style>
