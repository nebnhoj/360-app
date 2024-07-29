<template>
    <div ref="viewer" class="border-2 " :style="{ width: width, height: height }"></div>
  </template>
  
  <script setup>
  import * as THREE from 'three';
  import { ref, onMounted } from 'vue';
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls';
  
  const props = defineProps({
    imageUrl: { type: String, required: true },
    width: { type: String, default: '1920px' },
    height: { type: String, default: '1080px' },
  });
  
  const viewer = ref(null);
  
  onMounted(() => {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, viewer.value.clientWidth / viewer.value.clientHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ antialias: true });
    renderer.setSize(viewer.value.clientWidth, viewer.value.clientHeight);
    viewer.value.appendChild(renderer.domElement);
  
    const geometry = new THREE.SphereGeometry(500, 60, 40);
    geometry.scale(-1, 1, 1);
  
    const textureLoader = new THREE.TextureLoader();
    textureLoader.load(props.imageUrl, (texture) => {
      const material = new THREE.MeshBasicMaterial({ map: texture });
      const mesh = new THREE.Mesh(geometry, material);
      scene.add(mesh);
  
      const controls = new OrbitControls(camera, renderer.domElement);
      controls.enableZoom = true; // Enable zoom
      controls.enablePan = false; // Disable pan, if you only want to rotate and zoom
      controls.minDistance = 0.1;
      controls.maxDistance = 1000;
      controls.rotateSpeed = -0.25; // Reverse direction and slow down speed
      controls.autoRotate = false; // Disable auto rotation
  
      // Set initial position to look at the center
      camera.position.set(0, 0, 0.1);
  
      const animate = () => {
        requestAnimationFrame(animate);
        controls.update(); // Required for damping to work
        renderer.render(scene, camera);
      };
      animate();
  
      // Adjust camera and renderer on window resize
      window.addEventListener('resize', () => {
        const width = viewer.value.clientWidth;
        const height = viewer.value.clientHeight;
        renderer.setSize(width, height);
        camera.aspect = width / height;
        camera.updateProjectionMatrix();
      });
    });
  });
  </script>
  
  <style scoped>
   
  </style>
  