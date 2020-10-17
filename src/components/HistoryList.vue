<template>
  <div>
    <h1>Action History</h1>
    <History
      v-for="(item, index) in history"
      :historyItem="item"
      :historyItemIndex="index"
      :key="index"
      @onTimeTravel="onTimeTravel"
    />
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
      this.$emit('onTimeTravel', historyItemIndex);
    },
  },
  components: {
    History,
  },
};
</script>

<style scoped>
</style>
