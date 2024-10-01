<script>
import axios from "axios";
export default {
  name: "PosterPage",
  data() {
    return {
      posts: [],
      categories: [],
      types: [],
    };
  },
  methods: {
    getApi(urlApi) {
      axios
        .get(urlApi)
        .then((response) => {
          this.posts = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  mounted() {
    this.getApi("http://127.0.0.1:8000/api/posts");
  },
};
</script>
<template>
  <div class="container">
    <div class="row">
      <div class="col-8">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">Id</th>
              <th scope="col">Title</th>
              <th scope="col">Category</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(post, index) in posts.data" :key="index">
              <td>{{ post.id }}</td>
              <td>{{ post.title }}</td>
              <td>{{ post.category?.name ? post.category.name : "-" }}</td>
            </tr>
          </tbody>
        </table>
        <button
          class="btn btn-primary"
          v-for="(link, index) in posts.links"
          :key="index"
          v-html="link.label"
          @click="getApi(link.url)"
          :disabled="active"
        ></button>
      </div>
      <div class="col-4">colonna dei tipi e categorie</div>
    </div>
  </div>
</template>
<style lang='scss' scoped>
// @use 'path' as *;
</style>