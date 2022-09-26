<template>
  <div ref='canvasLine' class="canvas">
  </div>
</template>

<script>
import * as THREE from 'three'

export default {
  name: 'LineCanvas',
  data: function () {
    const scene = new THREE.Scene()
    const camera = new THREE.PerspectiveCamera(
      45,
      5000 / 500,
      1,
      500
    );
    const renderer = new THREE.WebGLRenderer();
    const materialLine = new THREE.LineBasicMaterial({ color: 0x0000ff })
    const points = [new THREE.Vector3(- 10, 0, 0), new THREE.Vector3(0, 10, 0), new THREE.Vector3(10, 0, 0)];
    const geometryLine = new THREE.BufferGeometry().setFromPoints(points);
    const line = new THREE.Line(geometryLine, materialLine)
    return {
      sceneLine: scene,
      cameraLine: camera,
      rendererLine: renderer,
      line: line,
      speed: 0.01
    }
  },
  created: function () {
    this.sceneLine.add(this.line)
    this.rendererLine.setSize(1000, 500)
    this.cameraLine.position.set(0, 0, 100);
    this.cameraLine.lookAt(0, 0, 0);
    this.sceneLine.background = new THREE.Color('hsl(0, 100%, 100%)')
  },
  mounted: function () {
    this.$refs.canvasLine.appendChild(this.rendererLine.domElement)
    this.animate()
  },
  methods: {
    animate: function () {
      this.rendererLine.render(this.sceneLine, this.cameraLine);
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
