<template>
  <div id="wrapper">
    <Layout>
      <Sider hide-trigger class="sider">
        <JsonHistory ref="jsonHistory" @onReadJson="onReadJson"></JsonHistory>
      </Sider>
      <Layout>
        <Content>
          <div class="content-height-offset"></div>
          <Tabs value="json-form">
            <TabPane label="Text" name="json-form">
              <JsonForm
                ref="jsonForm"
                @parseJson="onParseJson"
                @saveJson="onSaveJson"
              ></JsonForm>
            </TabPane>
            <TabPane label="Viewer" name="tree-view">
              <TreeView ref="treeView"></TreeView>
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
  components: { JsonForm, TreeView, JsonHistory },
  methods: {
    onParseJson(obj) {
      this.$refs.treeView.parseJson(obj);
    },
    onSaveJson(obj) {
      this.$refs.jsonHistory.saveJson(obj);
    },
    onReadJson(json) {
      this.$refs.jsonForm.onReadJson(json);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Source+Sans+Pro");

body {
  font-family: "Source Sans Pro", sans-serif;
}

#wrapper {
  /* padding: 10px; */
  height: auto;
}

.ivu-layout-sider-children,
.ivu-layout-content {
  background-color: #fff;
}

.content-height-offset {
  height: 16px;
}

::-webkit-scrollbar-track-piece {
  -webkit-border-radius: 0;
}
::-webkit-scrollbar {
  width: 5px;
  height: 10px;
}
::-webkit-scrollbar-thumb {
  height: 50px;
  background-color: #b8b8b8;
  -webkit-border-radius: 6px;
  outline-offset: -2px;
  filter: alpha(opacity = 50);
  -moz-opacity: 0.5;
  -khtml-opacity: 0.5;
  opacity: 0.5;
}
::-webkit-scrollbar-thumb:hover {
  height: 50px;
  background-color: #878987;
  -webkit-border-radius: 6px;
}
</style>
