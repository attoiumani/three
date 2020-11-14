<template>
  <div ref="lottieDiv" id="lottie"></div>
</template>

<script>
import lottie from "lottie-web";

export default {
  props: {
    options: {
      type: Object,
      required: true
    }
  },
  mounted() {
    this.anim = lottie.loadAnimation({
      container: this.$refs.lottieDiv,
      renderer: "svg",
      loop: this.options.loop !== false,
      autoplay: this.options.autoplay !== false,
      animationData: this.options.animationData,
      rendererSettings: this.options.rendererSettings
    });
    this.$emit("animCreated", this.anim);
  }
};
</script>

<style>
#lottie {
  width: 400px;
  margin: 0 auto;
}
</style>

