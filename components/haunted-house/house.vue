<script setup lang="ts">
// import { useTexture } from "@tresjs/core";
// import { Float32BufferAttribute } from "three";
// import { shallowRef, watch } from "vue";

// const brickTextures = await useTexture({
//   map: "../assets/haunted-house/bricks/color.jpg",
//   normalMap: "../assets/haunted-house/bricks/normal.jpg",
//   roughnessMap: "../assets/haunted-house/bricks/roughness.jpg",
//   ambientOcclusion: "../assets/haunted-house/bricks/ambientOcclusion.jpg",
// });

// const doorRef = shallowRef();

// const doorTextures = await useTexture({
//   map: "../assets/haunted-house/door/color.jpg",
//   alphaMap: "../assets/haunted-house/door/alpha.jpg",
//   ambientOcclusion: "../assets/haunted-house/door/ambientOcclusion.jpg",
//   displacementMap: "../assets/haunted-house/door/height.jpg",
//   normalMap: "../assets/haunted-house/door/normal.jpg",
//   metalnessMap: "../assets/haunted-house/door/metalness.jpg",
//   roughnessMap: "../assets/haunted-house/door/roughness.jpg",
// });

// const doorOptions = {
//   transparent: true,
//   displacementScale: 0.1,
//   map: doorTextures.map,
//   alphaMap: doorTextures.alphaMap,
//   aoMap: doorTextures.aoMap,
//   displacementMap: doorTextures.displacementMap,
//   normalMap: doorTextures.normalMap,
//   metalnessMap: doorTextures.metalnessMap,
//   roughnessMap: doorTextures.roughnessMap,
// };

// watch(doorRef, (value) => {
//   value.geometry.setAttribute(
//     "uv2",
//     new Float32BufferAttribute(value.geometry.attributes.uv.array, 2)
//   );
// });
</script>

<template>
  <TresGroup>
    <TresMesh :position="[0, 0.9, 2.01]">
      <TresPlaneGeometry :args="[2, 2, 100, 100]" />
      <TresMeshStandardMaterial />
    </TresMesh>
    <TresMesh :position="[0, 3, 0]" :rotation="[0, Math.PI * 0.25, 0]">
      <TresConeGeometry :args="[3.5, 1, 4]" />
      <TresMeshStandardMaterial color="#b35f45" />
    </TresMesh>
    <TresMesh :position="[0, 1.25, 0]" cast-shadow>
      <TresBoxGeometry :args="[4, 2.5, 4]" />
      <TresMeshStandardMaterial />
    </TresMesh>
    <TresPointLight
      :position="[0, 2.2, 2.7]"
      :args="['#ff7d46', 1, 7]"
      :shadow-mapSize-width="256"
      :shadow-mapSize-height="256"
      :shadow-camera-far="7"
      cast-shadow
    />
  </TresGroup>
</template>
