<template>
  <div id="root-wrapper">
    <div class="container">
      <div class="row">
        <div class="col-sm">
          <PostList :posts="posts" @onPostMove="onPostMove"></PostList>
        </div>
        <div class="col-sm">
          <HistoryList
            :history="history"
            @onTimeTravel="onTimeTravel"
          ></HistoryList>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PostList from "./components/PostList";
import HistoryList from "./components/HistoryList";

export default {
  name: "App",
  data() {
    return {
      posts: [],
      history: [],
    };
  },
  methods: {
    swapPost(postList, fromIndex, toIndex) {
      const toPost = postList[toIndex];
      if (toPost) {
        const fromPost = postList[fromIndex];
        postList[toIndex] = fromPost;
        postList[fromIndex] = toPost;
        return { movedPostId: fromPost.id, newPostList: postList };
      } else {
        return false;
      }
    },
    onPostMove(postIndex, action) {
      const fromIndex = postIndex;
      let toIndex = fromIndex;
      if (action === "up") {
        toIndex--;
      } else if (action === "down") {
        toIndex++;
      }
      if (fromIndex != toIndex) {
        const swapResponse = this.swapPost([...this.posts], fromIndex, toIndex);
        if (swapResponse) {
          this.posts = swapResponse.newPostList;
          this.history = [
            {
              title: `Moved post ${swapResponse.movedPostId} from ${fromIndex} index to ${toIndex} index`,
              date: new Date().getTime(),
              fromIndex,
              toIndex,
            },
            ...this.history,
          ];
        }
      }
    },
    onTimeTravel(historyItemIndex) {
      const historyListCopy = [...this.history];
      let postListCopy = [...this.posts];
      for (let i = 0; i <= historyItemIndex; i++) {
        const history = historyListCopy[i];
        const swapResponse = this.swapPost(
          postListCopy,
          history.toIndex,
          history.fromIndex
        );
        if (swapResponse) {
          postListCopy = swapResponse.newPostList;
        }
      }
      this.posts = postListCopy;
      this.history = historyListCopy.slice(
        historyItemIndex + 1,
        historyListCopy.length
      );
    },
  },
  components: {
    PostList,
    HistoryList,
  },
  created() {
    axios.get("https://jsonplaceholder.typicode.com/posts").then((response) => {
      if (response.data && Array.isArray(response.data)) {
        this.posts = response.data.slice(0, 5);
      }
    });
  },
};
</script>

<style scoped>
#root-wrapper {
  background: linear-gradient(
    172deg,
    #3949ab 0%,
    #3949ab 15%,
    #eeeeee 15%,
    #eeeeee 100%
  );
  padding: 15px;
}
</style>
