<template>
  <el-card style="max-width: 480px" id="btns">
    <p
      v-for="(item, index) in facilities"
      :key="index"
      class="text item"
      @click="flyTo(item.cameraOrt, item.cameraPosition)"
    >
      {{ item.name }}
    </p>
  </el-card>
  <!-- <div id="btns">
    <button
      v-for="(item, index) in facilities"
      :key="index"
      @click="flyTo(item.cameraOrt, item.cameraPosition)"
    >
      {{ item.name }}
    </button>
  </div> -->
  <div id="cesiumContainer"></div>
</template>

<script setup>
import * as Cesium from "cesium";
import { onMounted } from "vue";
import { load3dtiles, update3dtiles } from "/src/utils/load.js";
import facilities from "/src/assets/facilities.json";
let viewer;
Cesium.Ion.defaultAccessToken =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI5ZWZlNmFmNS0yNTkxLTQ2NzEtYjk4NS1lNGY5NWM1OTc5MmYiLCJpZCI6MjA1MTk1LCJpYXQiOjE3MTE2NzU4OTJ9.O9J1G_tirf33A-GKVOhxk1h9lWH08IZTnMOf-y8XS_U";

function flyTo(cameraOrt, cameraPosition) {
  let cameraOrtArr = cameraOrt.split(",");
  let cameraPositionArr = cameraPosition.split(",");
  viewer.camera.flyTo({
    destination: new Cesium.Cartesian3(...cameraPositionArr),
    orientation: {
      heading: cameraOrtArr[0],
      pitch: cameraOrtArr[1],
      roll: cameraOrtArr[2],
    },
    duration: 3,
  });
}

onMounted(() => {
  viewer = new Cesium.Viewer("cesiumContainer", {});
  load3dtiles(viewer, "/src/assets/b3dm/tileset.json", (tileset) => {
    update3dtiles(tileset);
    viewer.zoomTo(tileset);
  });
});
</script>

<style scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
#btns {
  width: 300px;
  position: fixed;
  left: 10px;
  top: 10px;
  z-index: 999;
}
</style>
