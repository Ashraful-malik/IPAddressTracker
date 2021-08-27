<template>
  <div id="app">
    <home />
  </div>
</template>

<script>
import home from "./components/Home.vue";

export default {
  name: "App",
  components: {
    home,
  },
};
</script>
<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
