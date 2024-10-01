<script>
import { store } from "../store";
import axios from "axios";
export default {
  name: "PosterPage",
  data() {
    return {
      store,
      linkUrl: "",
      posts: [],
      categories: [],
      types: [],
    };
  },
  methods: {
    getApi(urlApi, type) {
      let urlRequest = urlApi + type;
      axios
        .get(urlRequest)
        .then((response) => {
          if (type === "posts") {
            this.posts = response.data;
          } else {
            this[type] = response.data;
          }
          // attivo il bottone delle pagine
          this.linkUrl = urlApi;
        })
        .catch((error) => {
          console.log("Errore: ", error);
        });
    },
  },
  mounted() {
    this.getApi(this.store.urlPath, "posts");
    this.getApi(this.store.urlPath, "categories");
    this.getApi(this.store.urlPath, "types");
    // this.getApi("http://127.0.0.1:8000/api/categories");
    // this.getApi("http://127.0.0.1:8000/api/types");
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
              <th scope="col">Tipi</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(post, index) in posts.data" :key="index">
              <td>{{ post.id }}</td>
              <td>{{ post.title }}</td>
              <td>{{ post.category?.name ? post.category.name : "-" }}</td>
              <td class="typeColumn">
                <span v-for="(type, index) in post.types" :key="index">{{
                  type.name
                }}</span>
              </td>
            </tr>
          </tbody>
        </table>
        <button
          class="btn btn-primary"
          v-for="(link, index) in posts.links"
          :key="index"
          v-html="link.label"
          @click="getApi(link.url)"
          :class="{ active: link.url === linkUrl }"
        ></button>
      </div>
      <div class="col-4 d-flex flex-column gap-5">
        <div>
          <button
            class="btn btn-dark"
            v-for="(category, index) in categories"
            :key="index"
          >
            {{ category.name }}
          </button>
        </div>
        <div>
          <button
            class="btn btn-light"
            v-for="(type, index) in types"
            :key="index"
          >
            {{ type.name }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<style lang='scss' scoped>
// @use 'path' as *;
</style>