<template>
  <div id="app">
    <pixi/>
  </div>
</template>

<script>
import three from "@/components/three.vue";

export default {
  name: "app",
  components: {
    three
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style> 