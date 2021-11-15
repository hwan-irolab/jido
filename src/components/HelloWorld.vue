<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">Welcome to Vuetify</h1>

        <p class="subheading font-weight-regular">
          For help and collaboration with other Vuetify developers,
          <br />please join our online
          <a href="https://community.vuetifyjs.com" target="_blank"
            >Discord Community</a
          >
        </p>
      </v-col>

      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">What's next?</h2>

        <v-row justify="center">
          <a
            v-for="(next, i) in whatsNext"
            :key="i"
            :href="next.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ next.text }}
          </a>
        </v-row>
      </v-col>

      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">Important Links</h2>

        <v-row justify="center">
          <a
            v-for="(link, i) in importantLinks"
            :key="i"
            :href="link.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ link.text }}
          </a>
        </v-row>
      </v-col>

      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">Ecosystem</h2>

        <v-row justify="center">
          <a
            v-for="(eco, i) in ecosystem"
            :key="i"
            :href="eco.href"
            class="subheading mx-3"
            target="_blank"
          >
            {{ eco.text }}
          </a>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <div id="container"></div>
    </v-row>
  </v-container>
</template>

<script>
import * as THREE from "three";
import * as OrbitControls from "three-orbitcontrols";

export default {
  name: "HelloWorld",

  data: () => ({
    ecosystem: [
      {
        text: "vuetify-loader",
        href: "https://github.com/vuetifyjs/vuetify-loader",
      },
      {
        text: "github",
        href: "https://github.com/vuetifyjs/vuetify",
      },
      {
        text: "awesome-vuetify",
        href: "https://github.com/vuetifyjs/awesome-vuetify",
      },
    ],
    importantLinks: [
      {
        text: "Documentation",
        href: "https://vuetifyjs.com",
      },
      {
        text: "Chat",
        href: "https://community.vuetifyjs.com",
      },
      {
        text: "Made with Vuetify",
        href: "https://madewithvuejs.com/vuetify",
      },
      {
        text: "Twitter",
        href: "https://twitter.com/vuetifyjs",
      },
      {
        text: "Articles",
        href: "https://medium.com/vuetify",
      },
    ],
    whatsNext: [
      {
        text: "Explore components",
        href: "https://vuetifyjs.com/components/api-explorer",
      },
      {
        text: "Select a layout",
        href: "https://vuetifyjs.com/getting-started/pre-made-layouts",
      },
      {
        text: "Frequently Asked Questions",
        href: "https://vuetifyjs.com/getting-started/frequently-asked-questions",
      },
    ],
  }),

  methods: {
    init: function () {
      var windowWidth = 600; // window.innerWidth
      var windowHeight = 400; // window.innerHeight

      console.log("windowWidth : " + windowWidth);
      console.log("windowHeight : " + windowHeight);

      const scene = new THREE.Scene();
      const camera = new THREE.PerspectiveCamera(
        45,
        windowWidth / windowHeight,
        1,
        500
      );
      camera.position.set(0, 0, 100);
      camera.lookAt(0, 0, 0);

      const renderer = new THREE.WebGLRenderer();
      renderer.setSize(windowWidth, windowHeight);
      document.getElementById("container").appendChild(renderer.domElement);

      const geometry = new THREE.BoxGeometry(1, 1, 1);
      const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
      const cube = new THREE.Mesh(geometry, material);
      scene.add(cube);

      // draw line
      const lineMaterial = new THREE.LineBasicMaterial({ color: 0x0000ff });
      const points = [];
      points.push(new THREE.Vector3(-10, 0, 0));
      points.push(new THREE.Vector3(0, 10, 0));
      points.push(new THREE.Vector3(10, 0, 0));

      const lineGeometry = new THREE.BufferGeometry().setFromPoints(points);
      const line = new THREE.Line(lineGeometry, lineMaterial);

      camera.position.z = 5;

      scene.add(line);
      // renderer.render(this.scene, this.camera);

      const controls = new OrbitControls(camera, renderer.domElement);
      controls.rotateSpeed = 1.0; // 마우스로 카메라를 회전시킬 속도입니다. 기본값(Float)은 1입니다.
      controls.zoomSpeed = 1.2; // 마우스 휠로 카메라를 줌 시키는 속도 입니다. 기본값(Float)은 1입니다.
      controls.panSpeed = 0.8; // 패닝 속도 입니다. 기본값(Float)은 1입니다.
      controls.minDistance = 5; // 마우스 휠로 카메라 거리 조작시 최소 값. 기본값(Float)은 0 입니다.
      controls.maxDistance = 100;
      controls.update();

      function animate() {
        requestAnimationFrame(animate);

        renderer.render(scene, camera);
        controls.update(); // 마우스로인해 변경된 카메라값을 업데이트 합니다.
      }

      animate();

      // const controls = new OrbitControls(
      //   this.camera,
      //   this.renderer.domElement
      // );
      // controls.enableDamping = true;
      // controls.dampingFactor = 0.25;
      // controls.enableZoom = false;
      // controls.update();

      // function animate() {
      //   requestAnimationFrame(animate);

      //   // required if controls.enableDamping or controls.autoRotate are set to true
      //   controls.update();

      //   this.renderer.render(this.scene, this.camera);
      // }

      // animate()
    },
  },
  mounted() {
    this.init();
  },
};
</script>
