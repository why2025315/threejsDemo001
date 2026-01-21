<script setup lang="ts">
  import * as THREE from 'three';
 
  import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
   
  const width = window.innerWidth;
  const height = window.innerHeight;

  const camera = new THREE.PerspectiveCamera(70, width / height, 0.01, 10);
  camera.position.z = 1;


  const scene = new THREE.Scene();

  const axesHelper = new THREE.AxesHelper(150);
  scene.add(axesHelper);

  const geometry = new THREE.BoxGeometry(0.2, 0.2, 0.2);
  const material = new THREE.MeshNormalMaterial();

  const mesh = new THREE.Mesh(geometry, material);
  scene.add(mesh);

  // const pointLight = new THREE.PointLight(0xffffff, 1);
  // pointLight.intensity = 1.0;
  // pointLight.position.set(0, 1, 1);
  // scene.add(pointLight);

  // const DirectionalLight = new THREE.DirectionalLight(0xffffff, 1);
  // DirectionalLight.intensity = 1.0;
  // DirectionalLight.position.set(0, 1, 1);
  // scene.add(DirectionalLight);

  // const SpotLight = new THREE.SpotLight(0xffffff, 1);
  // SpotLight.intensity = 1.0;
  // SpotLight.position.set(0, 1, 1);
  // scene.add(SpotLight);

  const ambientLight = new THREE.AmbientLight(0xffffff, 1);
  scene.add(ambientLight);
  


  camera.lookAt(mesh.position);

  const renderer = new THREE.WebGLRenderer({
    antialias: true,
  });

  renderer.setSize(width, height);
  // renderer.setAnimationLoop(animate);

  document.body.appendChild(renderer.domElement);
  renderer.render(scene, camera);
  // function animate( time: number ) {
  //   mesh.rotation.x = time / 2000;
  //   mesh.rotation.y = time / 1000;

  //   mesh.rotation.z = time / 1000;

  //   renderer.render(scene, camera);
  // }

  const clock = new THREE.Clock();
  function render() {
    const spt = clock.getDelta() * 1000;
    console.log('两次渲染间隔spt(ms)', spt);
    console.log('帧率FPS', 1000 / spt)
    renderer.render(scene, camera);
    mesh.rotateY(0.01);
    requestAnimationFrame(render);
  }

  render();

  const controls = new OrbitControls(camera, renderer.domElement);
  controls.addEventListener('change', function () {
    renderer.render(scene, camera);
    console.log('camera.position', camera.position);
  });
</script>
<template>
  <div>
    <h1>ThreeDemo01</h1>
  </div>
</template>
