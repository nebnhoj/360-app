<template>
  <div ref="viewer" class="border-2" :style="{ width, height }"></div>
</template>

<script setup>
import * as THREE from 'three';
import { onBeforeUnmount, onMounted, ref } from 'vue';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';

const props = defineProps({
  imageUrl: { type: String, required: true },
  width: { type: String, default: '1920px' },
  height: { type: String, default: '1080px' },
});

const viewer = ref(null);

let renderer = null;
let camera = null;
let controls = null;
let frameId = null;

const handleResize = () => {
  if (!viewer.value || !renderer || !camera) {
    return;
  }

  const { clientWidth, clientHeight } = viewer.value;
  renderer.setSize(clientWidth, clientHeight);
  camera.aspect = clientWidth / clientHeight;
  camera.updateProjectionMatrix();
};

const animate = (scene) => {
  if (!renderer || !camera || !controls) {
    return;
  }

  controls.update();
  renderer.render(scene, camera);
  frameId = requestAnimationFrame(() => animate(scene));
};

onMounted(() => {
  if (!viewer.value) {
    return;
  }

  const scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(
    75,
    viewer.value.clientWidth / viewer.value.clientHeight,
    0.1,
    1000,
  );

  renderer = new THREE.WebGLRenderer({ antialias: true });
  viewer.value.appendChild(renderer.domElement);

  const geometry = new THREE.SphereGeometry(500, 60, 40);
  geometry.scale(-1, 1, 1);

  const textureLoader = new THREE.TextureLoader();
  textureLoader.load(props.imageUrl, (texture) => {
    const material = new THREE.MeshBasicMaterial({ map: texture });
    const mesh = new THREE.Mesh(geometry, material);
    scene.add(mesh);

    if (!camera || !renderer) {
      return;
    }

    controls = new OrbitControls(camera, renderer.domElement);
    controls.enableZoom = true;
    controls.enablePan = false;
    controls.minDistance = 0.1;
    controls.maxDistance = 1000;
    controls.rotateSpeed = -0.25;
    controls.autoRotate = false;

    camera.position.set(0, 0, 0.1);

    handleResize();
    animate(scene);
    window.addEventListener('resize', handleResize);
  });
});

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize);

  if (frameId !== null) {
    cancelAnimationFrame(frameId);
  }

  controls?.dispose();
  renderer?.dispose();
});
</script>
