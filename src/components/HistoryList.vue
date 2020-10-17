<template>
  <div class="card card-body">
    <div id="heading">
      <h5>Action History</h5>
      <p v-if="history.length === 0">
        Move some posts to generate history . . .
      </p>
    </div>
    <History
      v-for="(item, index) in history"
      :historyItem="item"
      :historyItemIndex="index"
      :key="index"
      @onTimeTravel="onTimeTravel"
    ></History>
  </div>
</template>

<script>
import History from "./History";

export default {
  name: "HistoryList",
  props: {
    history: Array,
  },
  methods: {
    onTimeTravel(historyItemIndex) {
      this.$emit("onTimeTravel", historyItemIndex);
    },
  },
  components: {
    History,
  },
};
</script>

<style scoped>
div {
  padding: 15px;
}
#heading {
  margin: 15px;
}
</style>
