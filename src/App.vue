<template>
  <div id="app">
    <ProductDisplay />
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";

export default {
  name: "App",
  components: {
    ProductDisplay,
  },
};
</script>

<style>
@import "./assets/style/page.css";
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap");
</style>
