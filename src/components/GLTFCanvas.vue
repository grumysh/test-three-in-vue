<template>
  <div ref='canvasGLTF' class="canvas">
  </div>
</template>

<script>
import * as THREE from 'three'
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'


export default {
  name: 'GLTFCanvas',
  data: function () {
    const scene = new THREE.Scene()
    const camera = new THREE.PerspectiveCamera(
      40,
      1000 / 1000,
      1,
      100
    );
    const renderer = new THREE.WebGLRenderer({ antialias: true })
    const loader = new GLTFLoader();
    const hemiLight = new THREE.HemisphereLight(0xffffff, 0xffffff, 0.6);
    const controls = new OrbitControls(camera, renderer.domElement);

    return {
      sceneGLTF: scene,
      cameraGLTF: camera,
      rendererGLTF: renderer,
      loader: loader,
      hemiLight: hemiLight,
      controls: controls,
      speed: 0.01
    }
  },
  created: function () {
    //se definen propiedades del render
    this.rendererGLTF.setSize(1000, 1000);
    this.rendererGLTF.toneMapping = THREE.ACESFilmicToneMapping;
    this.rendererGLTF.toneMappingExposure = 1;
    this.rendererGLTF.outputEncoding = THREE.sRGBEncoding;


    //posicionando la Camara
    this.cameraGLTF.position.set(5, 2, 8);

    //Definicion de las luces del entorno.
    this.hemiLight.color.setHSL(0.6, 1, 0.6);
    this.hemiLight.groundColor.setHSL(0.095, 1, 0.75);
    this.hemiLight.position.set(0, 50, 0);

    // Agrega propiedades a la escena
    this.sceneGLTF.add(this.hemiLight);
    this.sceneGLTF.background = new THREE.Color('hsl(0, 100%, 100%)')

    //Carga el asset.
    this.loader.load('../assets/Fished.gltf', (gltf) => {
      const model = gltf.scene;
      model.position.set(0, -2.5, 0);
      model.rotation.set(0, 35, 0);
      model.scale.set(0.1, 0.1, 0.1);
      this.sceneGLTF.add(model);
    })

    //Definicion de controles:
    this.controls.minDistance = 1;
    this.controls.maxDistance = 40;
    this.controls.target.set(0, 0, 0);
    this.controls.enableZoom = false
    this.controls.update();


  },
  mounted: function () {
    this.renderGLTF()
    this.$refs.canvasGLTF.appendChild(this.rendererGLTF.domElement)
  },
  methods: {
    renderGLTF: function () {
      requestAnimationFrame(this.renderGLTF.bind(this));
      this.rendererGLTF.render(this.sceneGLTF, this.cameraGLTF)
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
