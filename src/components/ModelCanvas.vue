<template>
  <div>
    <canvas id="c" width="500" height="450"></canvas>
  </div>
</template>

<script>
import * as THREE from 'three';
import {GLTFLoader} from 'three/examples/jsm/loaders/GLTFLoader';
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls';
import {ElLoading} from 'element-plus'

const manager = new THREE.LoadingManager();
const gltfLoader = new GLTFLoader(manager);
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(75, 1, 0.1, 1000);
const loadingInstance = ElLoading.service({fullscreen: true})

export default {
  name: "ModelCanvas",
  props: {
    gpsRollAxis: Number,
    gpsPitchAxis: Number,
    gpsYawAxis: Number,
  },
  mounted() {
    const canvas = document.querySelector('#c')
    this.renderer = new THREE.WebGLRenderer({canvas});
    this.controls = new OrbitControls(camera, this.renderer.domElement);
    camera.position.set(-30, 30, 0);
    camera.setFocalLength(50)
    this.controls.update();

    scene.background = new THREE.Color(0.8, 0.8, 0.8)

    const color = 0xFFFFFF;
    const light = new THREE.AmbientLight(color, 0.3);
    scene.add(light);

    const directionLight1 = new THREE.DirectionalLight(color, 0.8)
    directionLight1.position.set(-10, 10, 10)
    scene.add(directionLight1)

    const directionLight2 = new THREE.DirectionalLight(color, 0.5)
    directionLight2.position.set(-10, -10, -10)
    scene.add(directionLight2)

    camera.position.z = 5;

    manager.onLoad = () => {
      loadingInstance.close()
    }

    this.loadGPS()
    this.loadQuad()

    this.animate()
  },
  methods: {
    loadQuad() {
      gltfLoader.load("/models/quad.gltf", model => {
        const quad = new THREE.Group()
        quad.add(model.scene)
        const scaleFactor = 3
        quad.scale.set(scaleFactor, scaleFactor, scaleFactor)
        quad.traverse(child => {
          if (child.material) child.material.metalness = 0;
        })
        quad.rotation.y = Math.PI / 2
        scene.add(quad)
      })
    },
    loadGPS() {
      gltfLoader.load("/models/Beitian-BN880.gltf", model => {
        this.gps = new THREE.Group()
        this.gps.add(model.scene)
        const scaleFactor = 0.13
        this.gps.scale.set(scaleFactor, scaleFactor, scaleFactor)
        this.gps.position.x += 8
        this.gps.traverse(child => {
          if (child.material) child.material.metalness = 0;
        })
        this.gps.rotation.y = 3 * Math.PI / 2
        scene.add(this.gps)
      })
    },
    animate() {
      requestAnimationFrame(this.animate)

      if (this.gps) {
        this.gps.rotation.x = THREE.Math.degToRad(this.gpsPitchAxis);
        this.gps.rotation.y = THREE.Math.degToRad(this.gpsYawAxis);
        this.gps.rotation.z = THREE.Math.degToRad(this.gpsRollAxis);
      }


      if (this.controls)
        this.controls.update();

      this.renderer.render(scene, camera)
    }
  }
}


</script>

<style scoped>

</style>