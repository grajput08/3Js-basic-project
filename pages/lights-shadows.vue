<script setup lang="ts">
import { ref } from "vue";
import { OrbitControls } from "@tresjs/cientos";
import { TresCanvas, useRenderLoop } from "@tresjs/core";
import { BasicShadowMap, SRGBColorSpace, NoToneMapping } from "three";

const gl = {
  clearColor: "#82DBC5",
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping,
};

const boxRef = ref<any>();

const { onLoop } = useRenderLoop();

onLoop(() => {
  if (boxRef.value) {
    boxRef.value.rotation.y += 0.01;
  }
});
</script>

<template>
  <TresCanvas v-bind="gl" window-size>
    <OrbitControls />
    <TresPerspectiveCamera
      :position="[5, 7.5, 7.5]"
      :fov="45"
      :aspect="1"
      :near="0.1"
      :far="1000"
    />
    <OrbitControls />
    <TresMesh :position="[-2, 2, 0]" :rotation="[0, Math.PI, 0]">
      <TresConeGeometry :args="[1, 1.5, 3]" />
      <TresMeshToonMaterial color="#82DBC5" />
    </TresMesh>
    <TresMesh ref="boxRef" cast-shadow :position="[0, 0, 0]">
      <TresBoxGeometry :args="[1.5, 1.5, 1.5]" />
      <TresMeshToonMaterial color="#4F4F4F" />
    </TresMesh>
    <TresMesh cast-shadow :position="[2, -2, 0]">
      <TresSphereGeometry />
      <TresMeshToonMaterial color="#FBB03B" />
    </TresMesh>
    <TresMesh
      receive-shadow
      :position="[0, -3, 0]"
      :rotation="[-Math.PI / 2, 0, 0]"
    >
      <TresPlaneGeometry :args="[10, 10, 10, 10]" />
      <TresMeshStandardMaterial color="#f7f7f7" />
    </TresMesh>
    <TresAmbientLight color="#b9d5ff" :intensity="0.3" />
    <TresDirectionalLight
      :args="['#b9d5ff', 1.12]"
      :position="[4, 5, -2]"
      :shadow-mapSize-width="256"
      :shadow-mapSize-height="256"
      :shadow-camera-far="15"
      cast-shadow
    />
  </TresCanvas>
</template>
