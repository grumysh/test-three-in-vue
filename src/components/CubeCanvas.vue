<template>
  <div ref='canvas' class="canvas">
  </div>
</template>

<script>
import * as THREE from 'three'

export default {
  name: 'CubeCanvas',
  data: function () {
    const scene = new THREE.Scene()
    const camera = new THREE.PerspectiveCamera(
      75,
      1000 / 500,
      0.1,
      1000
    );
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    const geometry = new THREE.BoxGeometry(3, 3, 3);
    const material = new THREE.MeshBasicMaterial({ color: 0x3f67c0 });
    const cube = new THREE.Mesh(geometry, material);
    return {
      scene: scene,
      camera: camera,
      renderer: renderer,
      cube: cube,
      speed: 0.01
    }
  },
  created: function () {
    this.scene.add(this.cube)
    this.renderer.setSize(1000, 500)
    this.camera.position.z = 7
    this.scene.background = new THREE.Color('hsl(0, 100%, 100%)')
  },
  mounted: function () {
    this.$refs.canvas.appendChild(this.renderer.domElement)
    this.animate()
  },
  methods: {
    animate: function () {
      requestAnimationFrame(this.animate);
      this.cube.rotation.x += 0.005;
      this.cube.rotation.y += 0.005;
      this.renderer.render(this.scene, this.camera);
    }
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.canvas {
  width: 1000px;
  margin: auto;
}
</style>
