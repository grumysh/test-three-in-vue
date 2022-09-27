<template>
  <div id="app">
    <HelloWorld msg="Cube with Three.js in vue.js" />
    <CubeCanvas />
    <HelloWorld msg="Line with Three.js in vue.js" />
    <LineCanvas />
    <HelloWorld msg="GLTF with Three.js in vue.js" />
    <GLTFCanvas />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import CubeCanvas from './components/CubeCanvas.vue'
import LineCanvas from './components/LineCanvas.vue'
import GLTFCanvas from './components/GLTFCanvas.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
    CubeCanvas,
    LineCanvas,
    GLTFCanvas
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
