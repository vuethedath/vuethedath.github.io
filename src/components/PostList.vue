<template>
  <div>
    <h2 id="heading">Sortable Post List</h2>
    <Post
      v-for="(item, index) in posts"
      :post="item"
      :postIndex="index"
      :key="item.id"
      :showUp="index !== 0"
      :showDown="index + 1 < posts.length"
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
div {
  padding: 15px;
}
#heading {
  margin: 15px;
  color: white;
}
</style>
