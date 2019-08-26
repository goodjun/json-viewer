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
  mounted() {
    this.loadHistory();
    window.addEventListener("beforeunload", e => {
      this.saveHistory();
    });
  },
  methods: {
    saveJson(obj) {
      if (this.historys.length > 20) this.historys.pop();
      this.historys.unshift({
        id: this.$uuid.v4(),
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
    },
    saveHistory() {
      localStorage.setItem("json_history", JSON.stringify(this.historys));
    },
    loadHistory() {
      let jsonHistory = localStorage.getItem("json_history");
      if (jsonHistory) {
        jsonHistory = JSON.parse(jsonHistory);
        this.historys = jsonHistory;
      }
    }
  }
};
</script>

<style>
.ivu-card {
  margin-right: 10px;
}
</style>
