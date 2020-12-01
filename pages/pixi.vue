<template>
  <div id="filter"></div>
</template>

<script>
import * as PIXI from "pixi.js";
import { GlitchFilter } from "pixi-filters";

/*let PIXI;
if (process.client) {
  PIXI = require("pixi.js");
}*/

export default {
  data() {
    return {};
  },

  mounted() {
    const app = new PIXI.Application({
      width: 500,
      height: 500,
      backgroundColor: 0x000000,
    });
    const filterElement = document.getElementById("filter");

    filterElement.appendChild(app.view);
    app.loader
      .add("thumb", "https://front-note.net/dummy.png")
      .load((loader, resources) => {
        const thumb = new PIXI.Sprite(resources.thumb.texture);
        thumb.x = 100;
        thumb.y = 100;

        let fil = new PIXI.filters.GlitchFilter({
          slices: 10,
          offset: 100,
          fillMode: 1,
          speed: 0,
        });
        thumb.filters = [fil];
        app.stage.addChild(thumb);
        app.ticker.maxFPS = 1;
        app.ticker.add(() => {
          fil.slices = Math.floor(Math.random() * 10);
          fil.offset = Math.floor(Math.random() * 100);
        });
      });
  },
};
</script>