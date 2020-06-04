<template>
  <Card title="History" icon="ios-apps" :padding="0" shadow>
    <CellGroup @on-click="readJson" :style="{ height: height + 'px' }">
      <Cell
        v-for="history in historys"
        :name="history.id"
        :key="history.id"
        :title="history.title"
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
      historys: [],
      height: window.innerHeight - 60,
    };
  },
  mounted() {
    window.addEventListener("resize", (e) => {
      this.height = window.innerHeight - 60;
      e.preventDefault();
    });
    this.loadHistory();
    window.addEventListener("beforeunload", (e) => {
      this.saveHistory();
    });
  },
  methods: {
    saveJson(obj) {
      if (this.historys.length > 20) this.historys.pop();
      const jsonString = JSON.stringify(obj);
      this.historys.unshift({
        id: this.$uuid.v4(),
        title: jsonString.substr(0, 30),
        json: jsonString,
        date: this.$moment().format("YY-MM-DD HH:mm:ss"),
      });
    },
    readJson(index) {
      const findIndex = this.historys.findIndex((history) => {
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
    },
  },
};
</script>

<style>
.ivu-card {
  margin-right: 10px;
}
.ivu-cell-title {
  width: 170px;
  overflow: hidden;
  text-overflow: ellipsis;
}
.ivu-cell-group {
  overflow: overlay;
}
</style>
