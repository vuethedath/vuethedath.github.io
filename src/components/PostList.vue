<template>
  <div>
    <h1>Sortable Post List</h1>
    <Post
      v-for="(item, index) in posts"
      :post="item"
      :postIndex="index"
      :key="item.id"
      @onPostMove="onPostMove"
    />
  </div>
</template>

<script>
import Post from "./Post";

export default {
  name: "PostList",
  components: {
    Post,
  },
  methods: {
    onPostMove(postIndex, action) {
      this.$emit('onPostMove', postIndex, action);
    },
  },
  props: {
    posts: Array,
  },
};
</script>

<style scoped>
</style>
