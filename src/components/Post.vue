<template>
  <div>
    <h4>{{ post.id }}</h4>
    <h6>{{ post.title }}</h6>
    <p>{{ post.body }}</p>
    <button type="button" class="btn btn-success" @click="move('up')">Move Up</button>
    <button type="button" class="btn btn-danger" @click="move('down')">Move Down</button>
  </div>
</template>

<script>
export default {
  name: "Post",
  props: {
    post: Object,
    postIndex: Number,
  },
  methods: {
    move(action) {
      this.$emit('onPostMove', this.postIndex, action);
    },
  }
};
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
