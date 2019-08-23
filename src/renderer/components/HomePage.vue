<template>
  <div id="wrapper">
    <Tabs value="json-form">
      <TabPane label="Text" name="json-form">
        <JsonForm></JsonForm>
      </TabPane>
      <TabPane label="Viewer" name="tree-view">标签二的内容</TabPane>
    </Tabs>
  </div>
</template>

<script>
import JsonForm from "./JsonForm/JsonForm";

export default {
  name: "home-page",
  components: { JsonForm }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro");

body {
  font-family: "Source Sans Pro", sans-serif;
}

#wrapper {
  padding: 15px;
  height: auto;
}
</style>
