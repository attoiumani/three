<template>
  <div class="wrapper">
    <hr />

    <div id="wh" class="obj">1:width / height</div>
    <div id="xy" class="obj">2:x / y</div>
    <div id="scale" class="obj">3:scale / rotation</div>
    <div id="alpha" class="obj">4:alpha</div>
    <div id="bg" class="obj">5:bgColor</div>
  </div>
</template>

<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

if (process.client) {
  gsap.registerPlugin(ScrollTrigger);
}

export default {
  name: "HelloWorld",
  data() {
    return {};
  },
  mounted() {
    this.scrollItemA();

    // width / height：正の値、0、'**%'、'auto'で設定
    //gsap.to("#wh", 1.0, { width: "10%", height: 150 }); //

    // x軸移動 / y軸移動：正負の値、'**%'で設定
    gsap.to("#xy", 1.0, { x: "-10%", y: 100 }); //

    // 拡大・縮小 / 回転：倍率、角度で設定
    gsap.to("#scale", 1.0, { scale: 1.2, rotation: 225 }); //

    // 透明度：0〜1の値で設定。autoAlphaの場合、値が0になると同時にvisibilityがhiddenになる
    gsap.to("#alpha", 1.5, { autoAlpha: 0.1 }); //

    // 背景色：カラーコード、rgbaで設定
    gsap.to("#bg", 2.0, { backgroundColor: "#6A8CC7" }); //
  },

  methods: {
    scrollItemA() {
      gsap.to("#wh", {
        // 動かしたい要素は".b"
        x: 600, // 右方向に600動く
        rotation: 360, // 開始〜終了までの間で360度回転する
        duration: 1, // アニメーションは1秒間
        scrollTrigger: {
          trigger: "#wh", // 要素".b"がビューポートに入ったときにアニメーション開始
          start: "top center", // アニメーション開始位置
          end: "top 300px", // アニメーション終了位置
          scrub: true, // アニメーションをスクロール位置にリンクさせる
          markers: true, // マーカー表示
        },
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style>
.obj {
  position: relative;
  margin: 20px;
  padding: 5px;
  width: 70px;
  height: 70px;
  float: left;
}

#wh {
  background: #44a5cb;
  top: 1000px;
}
#xy {
  background: #da6272;
}
#scale {
  background: #f9db57;
}
#alpha {
  background: #23ac0e;
}
#bg {
  background: #b75c9d;
}

.wrapper {
  position: relative;
  width: 100%;
  height: 3000px;
}
</style>