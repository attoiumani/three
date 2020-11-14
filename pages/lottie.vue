<template>
  <div id="app">
    <div ref="lottie"></div>
  </div>
</template>

<script>
import lottie from "lottie-web";
import lottieData from "@/assets/animation/anima.json";

export default {
  name: "App",
  components: {},

  mounted() {
    this.lottie();
  },

  methods: {
    lottie() {
      lottie.loadAnimation({
        container: this.$refs.lottie,
        renderer: "canvas",
        loop: true,
        autoplay: true,
        animationData: lottieData,
      });
    },
  },
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
