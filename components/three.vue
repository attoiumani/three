<template>
  <div>
    <canvas id="canvas" width="600" height="400"></canvas>
    <NLink to="/test1" class="button--grey">About</NLink>
  </div>
</template>

<script>
import * as THREE from "three";
import TrackballControls from "three-trackballcontrols";

export default {
  name: "RotateBox",
  data() {
    const scene = new THREE.Scene();
    const renderer = null;
    const camera = new THREE.PerspectiveCamera(75, 600 / 400, 0.1, 1000);
    const light = new THREE.DirectionalLight(0xffffff);
    const geometry = new THREE.BoxGeometry(1, 1, 1);
    const material = new THREE.MeshNormalMaterial();
    const cube = new THREE.Mesh(geometry, material);
    return { scene, renderer, camera, light, geometry, material, cube };
  },
  mounted() {
    const $canvas = document.getElementById("canvas");
    // canvasを後付けで設定する方法あったら教えてほしいー
    this.renderer = new THREE.WebGLRenderer({
      antialias: true,
      canvas: $canvas,
    });

    this.camera.position.set(0, 0, 2);
    this.light.position.set(0, 0, 10);
    this.scene.add(this.cube);
    this.scene.add(this.light);

    this.controls = new TrackballControls(this.camera);
    this.controls.rotateSpeed = 1.0;
    this.controls.zoomSpeed = 5;
    this.controls.panSpeed = 0.8;
    this.controls.noZoom = false;
    this.controls.noPan = false;
    this.controls.staticMoving = true;
    this.controls.dynamicDampingFactor = 0.3;

    this.animate();
  },
  methods: {
    animate() {
      requestAnimationFrame(this.animate);

      //this.cube.rotation.x += 0.02;
      //this.cube.rotation.y += 0.02;

      this.renderer.render(this.scene, this.camera);
      this.controls.update();
    },
  },
};
</script>

<style></style>