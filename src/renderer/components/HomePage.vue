<template>
  <div id="wrapper">
    <Layout>
      <Sider hide-trigger class="sider">
        <JsonHistory></JsonHistory>
      </Sider>
      <Layout>
        <Content>
          <div class="content-height-offset"></div>
          <Tabs value="json-form">
            <TabPane label="Text" name="json-form">
              <JsonForm></JsonForm>
            </TabPane>
            <TabPane label="Viewer" name="tree-view">
              <TreeView></TreeView>
            </TabPane>
          </Tabs>
        </Content>
      </Layout>
    </Layout>
  </div>
</template>

<script>
import JsonForm from "./JsonForm/JsonForm";
import TreeView from "./TreeView/TreeView";
import JsonHistory from "./JsonHistory/JsonHistory";

export default {
  name: "home-page",
  components: { JsonForm, TreeView, JsonHistory }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro");

body {
  font-family: "Source Sans Pro", sans-serif;
}

#wrapper {
  padding: 10px;
  height: auto;
}

.ivu-layout-sider-children,
.ivu-layout-content {
  background-color: #fff;
}

.content-height-offset {
  height: 16px;
}
</style>
