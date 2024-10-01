<script>
import HeaderPage from "./views/partial/HeaderPage.vue";
export default {
  name: "App",
  data() {
    return {};
  },
  components: {
    HeaderPage,
  },
  methods: {},
};
</script>
<template>
  <HeaderPage />
  <main>
    <router-view></router-view>
  </main>
</template>
<style lang='scss' scoped>
// @use 'path' as *;
</style>