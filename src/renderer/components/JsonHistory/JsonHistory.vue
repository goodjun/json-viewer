<template>
  <Card title="History" icon="ios-apps" :padding="0" shadow>
    <CellGroup @on-click="readJson">
      <Cell
        v-for="history in historys"
        :name="history.id"
        :key="history.id"
        :title="history.json"
        :label="history.date"
      />
    </CellGroup>
  </Card>
</template>

<script>
export default {
  name: "json-history",
  data() {
    return {
      historys: []
    };
  },
  methods: {
    saveJson(obj) {
      this.historys.push({
        id: this.historys.length + 1,
        json: JSON.stringify(obj),
        date: this.$moment().format("YY-MM-DD HH:mm:ss")
      });
    },
    readJson(index) {
      const findIndex = this.historys.findIndex(history => {
        return history.id === index;
      });
      const json = this.historys[findIndex].json;
      this.$emit("onReadJson", json);
    }
  }
};
</script>

<style>
.ivu-card {
  margin-right: 10px;
}
</style>
