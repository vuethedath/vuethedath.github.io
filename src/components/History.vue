<template>
  <div>
    <h4>{{ historyItem.title }}</h4>
    <p>{{ historyItem.date }}</p>
    <button type="button" class="btn btn-warning" @click="timeTravel">Time Travel</button>
  </div>
</template>

<script>
export default {
  name: 'History',
  props: {
    historyItem: Object,
    historyItemIndex: Number,
  },
  methods: {
    timeTravel() {
      this.$emit('onTimeTravel', this.historyItemIndex);
    },
  }
}
</script>

<style scoped>
div {
  width: 500px;
  height: auto;
  margin: 20px;
  padding: 20px;
  background-color: gray;
}
</style>
