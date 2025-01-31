<script setup>
import { useTexture } from "@tresjs/core";

const texture = await useTexture({
  map: "/haunted-house/wall/castle_brick_broken_06_diff_1k.jpg",
  normalMap: "/haunted-house/wall/castle_brick_broken_06_nor_gl_1k.jpg",
  ambientOcclusion: "/haunted-house/wall/castle_brick_broken_06_arm_1k.jpg",
  metalnessMap: "/haunted-house/wall/castle_brick_broken_06_diff_1k.jpg",
});

const doorTextures = await useTexture({
  map: "/haunted-house/door/color.jpg",
  alphaMap: "/haunted-house/door/alpha.jpg",
  ambientOcclusion: "/haunted-house/door/ambientOcclusion.jpg",
  displacementMap: "/haunted-house/door/height.jpg",
  normalMap: "/haunted-house/door/normal.jpg",
  metalnessMap: "/haunted-house/door/metalness.jpg",
  roughnessMap: "/haunted-house/door/roughness.jpg",
});
</script>

<template>
  <TresGroup>
    <TresMesh :position="[0, 0.9, 2.01]">
      <TresPlaneGeometry :args="[2, 2, 100, 100]" />
      <TresMeshStandardMaterial
        v-bind="doorTextures"
        transparent
        :displacementScale="0.1"
      />
    </TresMesh>
    <TresMesh :position="[0, 3, 0]" :rotation="[0, Math.PI * 0.25, 0]">
      <TresConeGeometry :args="[3.5, 1, 4]" />
      <TresMeshStandardMaterial color="#82DBC5" v-bind="texture" />
    </TresMesh>
    <TresMesh :position="[0, 1.25, 0]" cast-shadow>
      <TresBoxGeometry :args="[4, 2.5, 4]" />
      <TresMeshStandardMaterial v-bind="texture" />
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
