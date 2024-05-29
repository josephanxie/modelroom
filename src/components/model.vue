<template>
  <div id="three-container"></div>
</template>

<script>
import * as THREE from 'three';

export default {
  mounted() {
    this.initThree();
  },
  methods: {
    initThree() {
      // 创建场景
      const scene = new THREE.Scene();
      window.addEventListener('resize', () => {
      
        // Update sizes
      sizes.width = window.innerWidth;
      sizes.height = window.innerHeight;

      // Update camera aspect ratio
      camera.aspect = sizes.width / sizes.height;
      camera.updateProjectionMatrix();

      // Update renderer
      renderer.setSize(sizes.width, sizes.height);
    }
  );

      // 创建相机
      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      camera.position.set(0, 0, 5);

      // 创建渲染器
      const renderer = new THREE.WebGLRenderer();
      renderer.setSize(window.innerWidth, window.innerHeight);
      document.getElementById('three-container').appendChild(renderer.domElement);

      // 添加一个立方体
      const geometry = new THREE.BoxGeometry();
      const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
      const cube = new THREE.Mesh(geometry, material);
      scene.add(cube);

      // 创建地面
      const floorMat = new THREE.MeshStandardMaterial({ color: 0xa9a9a9 });
      const floorGeometry = new THREE.BoxGeometry(300, 300, 0.01); // 长300，宽300，高0.01的长方体
      const floorMesh = new THREE.Mesh(floorGeometry, floorMat);
      floorMesh.receiveShadow = true; // 可以接收阴影
      floorMesh.rotation.x = -Math.PI / 2.0; // 将其旋转90度作为地面
      scene.add(floorMesh);
      floorMesh.receiveShadow = true;
     
      // 创建平行光
      const directionalLight = new THREE.DirectionalLight(0xffffff, 1.0); // 白色平行光，强度为默认值
      directionalLight.position.set(40, 40, 20); // 设置光源位置
      scene.add(directionalLight);
      renderer.shadowMap.enabled = true;//阴影

      // 渲染场景
      function animate() {
        requestAnimationFrame(animate);
        cube.rotation.x += 0.01;
        cube.rotation.y += 0.01;
        renderer.render(scene, camera);
      }
      animate();
    },
  },
};
</script>

<style>
#three-container {
  width: 100%;
  height: 100vh;
}
.webgl {
  position: fixed;
  top: 0;
  left: 0;
}
html, body {
  overflow: hidden;
}

</style>
