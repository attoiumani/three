<template>
  <div id="app"></div>
</template>

<script>
import * as PIXI from "pixi.js";
import { TweenLite } from "gsap";

const SIZE = 512;

PIXI.settings.SCALE_MODE = PIXI.SCALE_MODES.LINEAR;
PIXI.settings.PRECISION_FRAGMENT = PIXI.PRECISION.HIGH;
const DPR = window.devicePixelRatio && window.devicePixelRatio >= 2 ? 2 : 1;

export default {
  name: "App",
  mounted() {
    this.$options.slides = [];

    this.$options.app = new PIXI.Application({
      width: SIZE,
      height: SIZE,
      antialias: true,
      transparent: true,
      resolution: DPR,
      autoResize: true
    });

    const clipRect = new PIXI.Rectangle(
      0,
      0,
      this.$options.app.screen.width,
      this.$options.app.screen.height
    );

    this.$el.appendChild(this.$options.app.view);

    this.$options.stage = new PIXI.Container();
    this.$options.stage.filterArea = clipRect;

    this.$options.app.stage.addChild(this.$options.stage);

    const IMAGES = [
      "https://s3-us-west-2.amazonaws.com/s.cdpn.io/123024/j110.jpg",
      "https://s3-us-west-2.amazonaws.com/s.cdpn.io/123024/j104.jpg"
    ];

    this.$options.dispSprite = PIXI.Sprite.fromImage(
      "https://raw.githubusercontent.com/codrops/LiquidDistortion/master/img/dmaps/2048x2048/ripple_2.jpg"
    );

    this.$options.dispSprite.texture.baseTexture.wrapMode =
      PIXI.WRAP_MODES.REPEAT;
    this.$options.dispSprite.skew.x = 0;
    this.$options.dispSprite.skew.y = 0;
    this.$options.dispSprite.position.y = 0;
    this.$options.dispSprite.width = SIZE;
    this.$options.dispSprite.height = SIZE;

    this.$options.stage.addChild(this.$options.dispSprite);

    this.$options.dispFilter = new PIXI.filters.DisplacementFilter(
      this.$options.dispSprite,
      0
    );

    this.$options.dispFilter.scale.x = 15;
    this.$options.dispFilter.scale.y = 15;

    this.$options.stage.filters = [this.$options.dispFilter];

    try {
      PIXI.loader.add(IMAGES).load((l, images) => {
        Object.keys(images).forEach(key => {
          let sprite = new PIXI.Sprite(PIXI.loader.resources[key].texture);

          this.$options.slides.push(sprite);

          const SCALE = { x: SIZE / sprite.width, y: SIZE / sprite.height };
          sprite.scale.set(SCALE.x, SCALE.y);
          sprite.alpha = 0;
          this.$options.stage.addChild(sprite);
        });

        TweenLite.to(this.$options.slides[0], 0.575, {
          alpha: 1,
          onCompleted: () => {
            TweenLite.to(this.$options.slides[0], 0.575, {
              alpha: 0,
              delay: 2
            });

            TweenLite.to(this.$options.slides[1], 0.575, {
              alpha: 1,
              delay: 2
            });
          }
        });
      });
    } catch (e) {
      console.log(e);
    }

    this.render();
  },
  methods: {
    render() {
      this.$options.dispSprite.position.y += 4;
      // this.$options.dispSprite.rotation += 0.33 / 10;

      window.requestAnimationFrame(this.render.bind(this));
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
