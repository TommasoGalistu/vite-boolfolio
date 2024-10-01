<script>
export default {
  name: "HeaderPage",
  data() {
    return {};
  },
  methods: {},
};
</script>
<template>
  <nav>
    <router-link class="link" :to="{ name: 'home' }">Home</router-link>
    <router-link class="link" :to="{ name: 'about' }">About</router-link>
    <router-link class="link" :to="{ name: 'post' }">Post</router-link>
  </nav>
</template>
<style lang='scss' scoped>
// @use 'path' as *;
</style>