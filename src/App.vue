<template>
  <div id="cesiumContainer"></div>
</template>

<script setup>
import * as Cesium from "cesium";
import { onMounted } from "vue";
let viewer;
Cesium.Ion.defaultAccessToken =
  "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI5ZWZlNmFmNS0yNTkxLTQ2NzEtYjk4NS1lNGY5NWM1OTc5MmYiLCJpZCI6MjA1MTk1LCJpYXQiOjE3MTE2NzU4OTJ9.O9J1G_tirf33A-GKVOhxk1h9lWH08IZTnMOf-y8XS_U";
onMounted(() => {
  viewer = new Cesium.Viewer("cesiumContainer", {});
});
</script>

<style scoped>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>
