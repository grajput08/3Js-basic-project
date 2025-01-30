<script setup lang="ts">
import { onMounted, ref } from "vue";
import { TresCanvas } from "@tresjs/core";
import { OrbitControls, Sky, Grid } from "@tresjs/cientos";
import * as dat from "lil-gui"; // Import lil-gui

// Create reactive references for GUI controls
const lightIntensity = ref(1.2);
const cameraPosition = ref([-4.76, 3.78, 12]);
const coneColor = ref("#82DBC5");
const boxColor = ref("#4F4F4F");
const sphereColor = ref("#FBB03B");

// Sky parameters
const skyParams = ref({
  turbidity: 3.4,
  rayleigh: 3,
  mieCoefficient: 0.005,
  mieDirectionalG: 0.7,
  elevation: 0.6,
  azimuth: 180,
  distance: 450000,
});

// Sphere parameters
const sphereParams = ref({
  radius: 1,
  widthSegments: 32,
  heightSegments: 16,
  phiStart: 0,
  phiLength: Math.PI * 2,
  thetaStart: 0,
  thetaLength: Math.PI,
});

onMounted(() => {
  // Initialize the GUI
  const gui = new dat.GUI();

  // Add controls for light intensity, camera position, and colors
  gui.add(lightIntensity, "value", 0, 3).name("Light Intensity");
  gui.add(cameraPosition.value, 0, -10, 20).name("Camera X");
  gui.add(cameraPosition.value, 1, -10, 20).name("Camera Y");
  gui.add(cameraPosition.value, 2, -10, 20).name("Camera Z");
  gui.addColor(coneColor, "value").name("Cone Color");
  gui.addColor(boxColor, "value").name("Box Color");
  gui.addColor(sphereColor, "value").name("Sphere Color");

  // Add Sphere controls folder
  const sphereFolder = gui.addFolder("Sphere Settings");
  sphereFolder.add(sphereParams.value, "radius", 0.1, 3, 0.1).name("Radius");
  sphereFolder
    .add(sphereParams.value, "widthSegments", 3, 64, 1)
    .name("Width Segments");
  sphereFolder
    .add(sphereParams.value, "heightSegments", 2, 32, 1)
    .name("Height Segments");
  sphereFolder
    .add(sphereParams.value, "phiStart", 0, Math.PI * 2, 0.1)
    .name("Phi Start");
  sphereFolder
    .add(sphereParams.value, "phiLength", 0, Math.PI * 2, 0.1)
    .name("Phi Length");
  sphereFolder
    .add(sphereParams.value, "thetaStart", 0, Math.PI, 0.1)
    .name("Theta Start");
  sphereFolder
    .add(sphereParams.value, "thetaLength", 0, Math.PI, 0.1)
    .name("Theta Length");
  sphereFolder.open();

  const skyFolder = gui.addFolder("Sky Settings");
  skyFolder.add(skyParams.value, "turbidity", 0, 10, 0.1).name("Turbidity");
  skyFolder.add(skyParams.value, "rayleigh", 0, 10, 0.1).name("Rayleigh");
  skyFolder
    .add(skyParams.value, "mieCoefficient", 0, 0.1, 0.001)
    .name("Mie Coefficient");
  skyFolder
    .add(skyParams.value, "mieDirectionalG", 0, 1, 0.01)
    .name("Mie Direction");
  skyFolder
    .add(skyParams.value, "elevation", -90, 90, 0.1)
    .name("Sun Elevation");
  skyFolder.add(skyParams.value, "azimuth", 0, 360, 1).name("Sun Azimuth");
  skyFolder
    .add(skyParams.value, "distance", 1000, 1000000, 1000)
    .name("Distance");
  skyFolder.open();
});
</script>

<template>
  <TresCanvas window-size clear-color="#333">
    <TresPerspectiveCamera
      :position="[cameraPosition[0], cameraPosition[1], cameraPosition[2]]"
    />
    <Sky v-bind="skyParams" />
    <OrbitControls />
    <Grid
      :args="[10.5, 10.5]"
      cell-color="#82dbc5"
      :cell-size="0.6"
      :cell-thickness="0.5"
      section-color="#fbb03b"
      :section-size="2"
      :section-thickness="1.3"
      :infinite-grid="true"
      :fade-from="0"
      :fade-distance="12"
      :fade-strength="1"
    />
    <TresMesh :position="[2, -2, 0]" :rotation="[0, Math.PI, 0]">
      <TresConeGeometry :args="[1, 1.5, 3]" />
      <TresMeshToonMaterial :color="coneColor" />
    </TresMesh>
    <TresMesh :position="[0, 0, 0]" cast-shadow>
      <TresBoxGeometry :args="[1.5, 1.5, 1.5]" />
      <TresMeshToonMaterial :color="boxColor" />
    </TresMesh>
    <TresMesh :position="[-2, 2, 0]">
      <TresSphereGeometry
        :args="[
          sphereParams.radius,
          sphereParams.widthSegments,
          sphereParams.heightSegments,
          sphereParams.phiStart,
          sphereParams.phiLength,
          sphereParams.thetaStart,
          sphereParams.thetaLength,
        ]"
      />
      <TresMeshToonMaterial :color="sphereColor" />
    </TresMesh>
    <TresDirectionalLight
      :position="[0, 2, 4]"
      :intensity="lightIntensity"
      cast-shadow
    />
  </TresCanvas>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
#app {
  height: 100%;
  width: 100%;
  background-color: #000;
}
</style>
