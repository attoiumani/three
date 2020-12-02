<template>
<div>
  <canvas id ="canvas"></canvas>
</div>
</template>

<script>
import * as PIXI from "pixi.js";
import { GlitchFilter } from "pixi-filters";

export default {
  data() {
    return {
      imgPath: require(`@/assets/images/cr7.jpg`),
    };
  },

  mounted() {
    const app = new PIXI.Application({
      view: canvas,
    });
    document.body.appendChild(app.view);

    app.stage.interactive = true;

    const container = new PIXI.Container();
    app.stage.addChild(container);

    const glitchFilter = new GlitchFilter({
      slices: 10,
      offset: 100,
      fillMode: 1,
      speed: 0,
    });

    app.ticker.maxFPS = 1;
    app.ticker.add(function () {
      glitchFilter.offset = Math.floor(Math.random() * 100);
      glitchFilter.slices = Math.floor(Math.random() * 10);
    });

    const displacementSprite = PIXI.Sprite.from(this.imgPath);

    app.stage.addChild(displacementSprite);

    displacementSprite.filters = [glitchFilter];
  },
};
</script>