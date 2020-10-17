<template>
  <div id="history" class="card">
    <div class="card-body">
      <h5 class="card-title">
        {{ historyItem.title }}
      </h5>
      <p class="card-text">{{ Math.floor(((new Date()).getTime() - historyItem.date)/1000) }} seconds ago</p>
      <button type="button" class="btn btn-warning" @click="timeTravel">
        Time Travel
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "History",
  props: {
    historyItem: Object,
    historyItemIndex: Number,
  },
  methods: {
    timeTravel() {
      this.$emit("onTimeTravel", this.historyItemIndex);
    },
  },
};
</script>

<style scoped>
#history {
  margin: 8px;
}
</style>
