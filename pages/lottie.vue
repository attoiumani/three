<template>
  <div id="app">
    <LottieAnima :options="defaultOptions" v-on:animCreated="handleAnimation"/>
    <div>
      <p>Speed: x{{animationSpeed}}</p>
      <input
        type="range"
        value="1"
        min="0"
        max="3"
        step="0.5"
        v-on:change="onSpeedChange"
        v-model="animationSpeed"
      >
    </div>
    <button v-on:click="stop">stop</button>
    <button v-on:click="pause">pause</button>
    <button v-on:click="play">play</button>
  </div>
</template>

<script>
import LottieAnima from "@/components/LottieAnima";
import * as animationData from "@/anima.json";

export default {
  name: "App",
  components: {
    LottieAnima
  },
  data() {
    return {
      defaultOptions: { animationData: animationData },
      animationSpeed: 1
    };
  },
  methods: {
    handleAnimation: function(anim) {
      this.anim = anim;
    },
    stop: function() {
      this.anim.stop();
    },
    play: function() {
      this.anim.play();
    },
    pause: function() {
      this.anim.pause();
    },
    onSpeedChange: function() {
      this.anim.setSpeed(this.animationSpeed);
    }
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
