<template>
  <Card title="History" icon="ios-apps" :padding="0" shadow>
    <CellGroup>
      <Cell v-for="history in historys" :title="history.json" :label="history.datetime" />
    </CellGroup>
  </Card>
</template>

<script>
export default {
  name: "json-history",
  data() {
    return {
      historys: [
        { json: '{"name": "tom"}', datetime: "2019/08/22 19:39" },
        { json: '{"name": "tom"}', datetime: "2019/08/22 19:39" },
        { json: '{"name": "tom"}', datetime: "2019/08/22 19:39" },
        { json: '{"name": "tom"}', datetime: "2019/08/22 19:39" },
        { json: '{"name": "tom"}', datetime: "2019/08/22 19:39" },
        { json: '{"name": "tom"}', datetime: "2019/08/22 19:39" },
        { json: '{"name": "tom"}', datetime: "2019/08/22 19:39" }
      ]
    };
  }
};
</script>

<style>
.ivu-card {
  margin-right: 10px;
  height: 520px;
}
</style>
