<template lang="html">
  <div :class="'img-'+this.mainImgID" id="cvs_thumnails_box">
    <canvas id="cvs">
    </canvas>
    <div id="thumbnails">
      <div v-for="t in thumbnails" @click="changeImg(t.id)" :class="'thumbnail-'+ t.id" class="thumbnail">
      </div>
    </div>
  </div>
</template>

<script>
import {Container} from 'pixi.js'
import {WebGLRenderer} from 'pixi.js'
import {Sprite} from 'pixi.js'
import {Graphics} from 'pixi.js'
import {Filter} from 'pixi.js'
import {Matrix} from 'pixi.js'
export default {
  props: {
    'productId': Number
  },
  data: () => {
    return {
      mainImgID: 0,
      thumbnails: Array.apply(null, { length: 5 })
        .map(function (_, idx) {
          return {
            id: idx,
          }
        })
    }
  },
  mounted: function () {
    this.drawCanvas(this.mainImgID)
  },
  methods: {
    changeImg: function (imgID) {
      this.drawCanvas(imgID)
    },
    drawCanvas: function(imgID) {
      let cvs = document.getElementById('cvs')
      cvs.width = 800
      cvs.height = 540
      let renderer = new PIXI.WebGLRenderer(cvs.width, cvs.height, {backgroundColor : 0xffffff, view: cvs, antialias: true} )
      let container = new PIXI.Container()
      let img = new Image()
      img.src = "/images/detail/" + imgID + ".jpg";
      img.onload = function(){
        let sprite = new PIXI.Sprite(new PIXI.Texture(new PIXI.BaseTexture(img)))
        sprite.width = cvs.width
        sprite.height = cvs.height
        container.addChild(sprite)
        renderer.render(container)
      }
      let frag =
        `precision mediump float;
        uniform vec4 filterArea;
        uniform sampler2D uSampler;
        uniform float val;
        varying vec2 vTextureCoord;
        void main (void) {
          vec4 col = texture2D(uSampler, vTextureCoord);
          if(vTextureCoord.x > val) gl_FragColor = texture2D(uSampler, vec2(val, vTextureCoord.y));
          else                      gl_FragColor = col;
        }`.split('\n').reduce((c, a) => c + a.trim() + '\n')
      let uniforms = {
        val: { type: 'float', value: 0 }
      };
      let filter = new PIXI.Filter(null, frag, uniforms);
      container.filters = [filter]
      let count = 0;
      function update(){
        count += Math.pow(0.15 * Math.random(), 2);
        uniforms = {
          val: { type: 'float', value: count },
          mappedMatrix : { type: 'mat3', value: new PIXI.Matrix() }
        };
        filter = new PIXI.Filter(null, frag, uniforms);
        container.filters = [filter]
        renderer.render(container)
        requestAnimationFrame(update)
      }
      update();
    }
  }
}
</script>
