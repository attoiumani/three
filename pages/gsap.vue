<template>
  <canvas id="cv"></canvas>
</template>

<script>
import { TweenMax } from "gsap";
import * as PIXI from "pixi.js";

export default {
  data() {
    return {};
  },

  mounted() {
    let $container,
      $cv,
      items,
      vec = 0;

    function init_stage() {
      $cv = new PIXI.Application({
        width: $("#cv").width(),
        height: $("#cv").height(),
        antialias: true,
        transparent: true,
        autoResize: true,
        resolution: devicePixelRatio,
        backgroundColor: 0x000000,
        view: document.getElementById("cv"),
      });

      $container = new PIXI.Container();
      $cv.stage.addChild($container);

      $(window).on("load resize", function () {
        $cv.renderer.resize(window.innerWidth, window.innerHeight);
      });
    }

    function create_items(n) {
      items = [];
      for (var i = 0; i < n; i++) {
        var item = new PIXI.Graphics();
        item.x = centerX();
        item.y = centerY();
        item.scale.x = 0.1;
        item.scale.y = 0.1;
        items[i] = item;
        create_item_obj(items[i], 0xff0000);
        $container.addChild(items[i]);
        loop_motion(items[i]);
      }
    }
    /*
  var STAGE_H = $cv.view.height;
  var STAGE_W = $cv.view.width;
  $basegraphics.width = STAGE_W;
  $basegraphics.height = STAGE_H;
  $basegraphics.beginFill(0xFFFFFF);
  $basegraphics.scale.x = 1;
  $basegraphics.scale.y = 1;
  //$container.addChild($basegraphics);*/

    function loop_motion($obj) {
      $obj.x = centerX();
      $obj.y = centerY();
      $obj.scale.x = 0.1;
      $obj.scale.y = 0.1;
      vec += 25;
      const time = Math.random() * 5 + 5;
      const rota = Math.floor(Math.random() * 2) ? -0.01 : 0.01;

      TweenMax.to($obj, time, {
        x: randomX(),
        y: randomY(),
        ease: Power0.easeIn,
        onComplete: function () {
          loop_motion($obj);
        },
        onUpdate: function (tween) {
          var scale = tween.target.scale.x + 0.02;
          if (scale < 10) {
            $obj.scale.set(scale, scale);
          }
          $obj.rotation += rota;
        },
        onUpdateParams: ["{self}"],
      });
    }

    function randomX() {
      return Math.cos(vec * (Math.PI / 180.0)) * get_radius() + centerX();
    }

    function randomY() {
      return Math.sin(vec * (Math.PI / 180.0)) * get_radius() + centerY();
    }
    function centerX() {
      return $cv.screen.width * 0.5;
    }
    function centerY() {
      return $cv.screen.height * 0.5;
    }
    function get_radius() {
      return (
        Math.sqrt(
          Math.pow($cv.screen.height, 2) + Math.pow($cv.screen.width, 2)
        ) + 100
      );
    }
    function create_item_obj(item, col) {
      let w = 30;
      let h = 30;
      let k = Math.floor(Math.random() * 4);
      item.clear();
      if (k == 0) {
        item.beginFill(col);
        item.moveTo(w * 0.5, h);
        item.quadraticCurveTo(w, h * 0.8, w, h * 0.5);
        item.quadraticCurveTo(w, 0, w * 0.5, h * 0.25);
        item.quadraticCurveTo(0, 0, 0, h * 0.5);
        item.quadraticCurveTo(0, h * 0.8, w * 0.5, h);
      } else if (k == 1) {
        item.beginFill(col);
        item.moveTo(w * 0.5, 0);
        item.lineTo(w * 0.9, h * 0.5);
        item.lineTo(w * 0.5, h);
        item.lineTo(w * 0.1, h * 0.5);
      } else if (k == 2) {
        item.beginFill(0x000000);
        item.moveTo(w * 0.5, h);
        item.lineTo(w * 0.35, h);
        item.lineTo(w * 0.45, h * 0.7);
        item.quadraticCurveTo(-0.12 * w, h * 0.88, w * 0.1, h * 0.4);
        item.quadraticCurveTo(0.2 * w, h * 0.2, w * 0.5, 0);
        item.quadraticCurveTo(w * 0.8, h * 0.2, w * 0.9, h * 0.4);
        item.quadraticCurveTo(w * 1.12, h * 0.88, w * 0.55, h * 0.7);
        item.lineTo(w * 0.65, h);
        item.lineTo(w * 0.5, h);
      } else if (k == 3) {
        item.beginFill(0x000000);
        item.drawCircle(w * 0.5, h * 0.2, w * 0.22);
        item.drawCircle(w * 0.75, h * 0.52, w * 0.22);
        item.drawCircle(w * 0.25, h * 0.52, w * 0.22);
        item.moveTo(w * 0.5, h);
        item.lineTo(w * 0.35, h);
        item.lineTo(w * 0.5, h * 0.1);
        item.lineTo(w * 0.65, h);
        item.lineTo(w * 0.5, h);
      }
      item.endFill();
      item.position.x = -1 * w * 0.5;
      item.position.y = -1 * h * 0.5;
    }

    init_stage();
    create_items(80);
  },
};
</script>