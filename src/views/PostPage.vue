<script>
import axios from "axios";
export default {
  name: "PosterPage",
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    getApi() {
      axios
        .get("http://127.0.0.1:8000/api/posts")
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.getApi();
  },
};
</script>
<template>
  <h1 class="">PosterPage</h1>
</template>
<style lang='scss' scoped>
// @use 'path' as *;
</style>