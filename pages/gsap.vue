<template>
  <div>
<p class="code">TweenMax.to('#obj', 0.5, { left: 200 });</p>
<p class="note">「#obj」を「0.5」秒かけて「left」方向に「200」px アニメーションさせる</p>

<hr />

<div id="obj">obj</div>
  </div>
</template>

<script>
import { TweenLite, TweenMax, Power2, Back, Power4 } from "gsap";

export default {
  name: "HelloWorld",
  data() {
    return {
      user: {
        email: "",
        password: ""
      }
    };
  },
  mounted() {
//「#obj」を「0.5」秒かけて「left」方向に「200」px アニメーションさせる
TweenMax.to('#obj', 0.5, { left: 200 });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>

#obj {
  position: relative;
  width: 100px;
  height: 100px;
  background: #44A5CB;
  color: #fff;
}

/* text ----------- */
p { font-size: 80%; }
.note { font-size: 75%; color: rgba(0,0,0,0.8); }
</style>