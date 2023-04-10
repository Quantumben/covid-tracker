<template>
  <Header />
  <div class="container">
    <RouterView />
  </div>
</template>

<script>
// import { RouterLink, RouterView } from 'vue-router'
import Header from "@/components/Header.vue";

export default {
  name: "App",
  components: {
    Header,
  },
};
</script>
