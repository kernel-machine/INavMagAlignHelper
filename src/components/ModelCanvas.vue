<template>
  <div>
    <canvas id="c" width="650" height="450"></canvas>
  </div>
</template>

<script>
import * as THREE from 'three';
import {GLTFLoader} from 'three/examples/jsm/loaders/GLTFLoader';
import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls';
import {ElLoading} from 'element-plus'

const baseUrl = window.location.href;

const manager = new THREE.LoadingManager();
const gltfLoader = new GLTFLoader(manager);
const scene = new THREE.Scene();
const loadingInstance = ElLoading.service({fullscreen: true})

export default {
  name: "ModelCanvas",
  props: {
    gpsRollAxis: Number,
    gpsPitchAxis: Number,
    gpsYawAxis: Number,
    isShowGps: Boolean
  },
  mounted() {
    const canvas = document.querySelector('#c')
    this.renderer = new THREE.WebGLRenderer({canvas});
    this.camera = new THREE.PerspectiveCamera(70, canvas.width / canvas.height, 0.1, 1000);
    this.controls = new OrbitControls(this.camera, this.renderer.domElement);
    this.camera.position.set(-25, 35, 35);
    this.camera.setFocalLength(50)
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

    manager.onLoad = () => {
      loadingInstance.close()
    }

    this.loadGPS()
    this.loadQuad()
    this.loadXYZ()

    this.animate()
  },
  methods: {
    loadQuad() {
      gltfLoader.load(baseUrl + "/models/quad.gltf", model => {
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
      gltfLoader.load(baseUrl + "/models/Beitian-BN880.gltf", model => {
        this.gps = model.scene
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
    loadXYZ() {
      gltfLoader.load(baseUrl + "/models/xyz.gltf", model => {
        this.xyz = model.scene
        const scaleFactor = 0.15
        this.xyz.scale.set(scaleFactor, scaleFactor, scaleFactor)
        this.xyz.position.x += 10
        this.xyz.traverse(child => {
          if (child.material) child.material.opacity = 0.5;
        })
        scene.add(this.xyz)

      })
    },
    animate() {
      requestAnimationFrame(this.animate)

      if (this.gps) {
        this.gps.rotation.set(THREE.Math.degToRad(this.gpsPitchAxis), THREE.Math.degToRad(this.gpsYawAxis), THREE.Math.degToRad(this.gpsRollAxis), 'YXZ');
        this.gps.visible = this.isShowGps
      }

      if(this.xyz) {
        this.xyz.rotation.set(THREE.Math.degToRad(this.gpsPitchAxis), THREE.Math.degToRad(this.gpsYawAxis), THREE.Math.degToRad(this.gpsRollAxis), 'YXZ');
        this.xyz.visible = !this.isShowGps
      }

      if (this.controls)
        this.controls.update();

      if (this.camera != null)
        this.renderer.render(scene, this.camera)
    }
  }
}


</script>

<style scoped>

</style>