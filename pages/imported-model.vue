<script setup lang="ts">
import { GLTFModel, OrbitControls } from "@tresjs/cientos";
import { TresCanvas } from "@tresjs/core";
import { onMounted, ref } from "vue";
import GUI from "lil-gui";

const backgroundColor = ref("#F78B3D");
const selectedModel = ref("blender-cube.glb");

const models = {
  "Blender Cube": "blender-cube.glb",
  "Box Animated": "BoxAnimated.glb",
  "Carbon Fibre": "CarbonFibre.glb",
  "Cesium Man": "CesiumMan.glb",
  Robot: "RobotExpressive.glb",
};

onMounted(() => {
  const gui = new GUI();
  const params = {
    backgroundColor: backgroundColor.value,
    model: Object.keys(models)[0],
  };

  gui.addColor(params, "backgroundColor").onChange((value) => {
    backgroundColor.value = value;
  });

  gui.add(params, "model", Object.keys(models)).onChange((value) => {
    selectedModel.value = models[value];
  });
});
</script>

<template>
  <div class="scene-container">
    <TresCanvas :clear-color="backgroundColor">
      <TresPerspectiveCamera :position="[3, 2, 5]" />
      <OrbitControls />
      <Suspense>
        <GLTFModel :key="selectedModel" :path="`/models/${selectedModel}`" />
      </Suspense>
      <TresDirectionalLight :intensity="2" :position="[3, 3, 3]" />
      <TresAmbientLight :intensity="1" />
    </TresCanvas>
  </div>
</template>

<style scoped>
.scene-container {
  width: 100%;
  min-height: 100vh;
}
</style>
