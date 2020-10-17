<template>
  <div id="post" class="card">
    <div class="card-body">
      <h5 class="card-title">
        <span id="postId">{{ post.id }}</span
        >{{ post.title }}
      </h5>
      <p class="card-text">{{ post.body }}</p>
      <button v-if="showUp" id="buttons" type="button" class="btn btn-success" @click="move('up')">
        Move Up
      </button>
      <button v-if="showDown" id="buttons" type="button" class="btn btn-danger" @click="move('down')">
        Move Down
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Post",
  props: {
    post: Object,
    postIndex: Number,
    showUp: Boolean,
    showDown: Boolean,
  },
  methods: {
    move(action) {
      this.$emit("onPostMove", this.postIndex, action);
    },
  },
};
</script>

<style scoped>
#post {
  margin: 15px;
}
#postId {
  color: blueviolet;
  margin-right: 20px;
}
#buttons {
  margin-right: 15px;
}
</style>
