<script setup>
import { useTexture } from "@tresjs/core";
import { RepeatWrapping } from "three";

const configureTexture = async (pathConfig) => {
  const texture = await useTexture(pathConfig);
  Object.values(texture).forEach((map) => {
    if (map) {
      map.repeat.set(8, 8);
      map.wrapS = RepeatWrapping;
      map.wrapT = RepeatWrapping;
    }
  });
  return texture;
};

const floorTexture = await configureTexture({
  map: "/haunted-house/floor/coast_sand_rocks_02_diff_1k.jpg",
  normalMap: "/haunted-house/floor/coast_sand_rocks_02_nor_gl_1k.jpg",
  roughnessMap: "/haunted-house/floor/coast_sand_rocks_02_disp_1k.jpg",
  aoMap: "/haunted-house/floor/coast_sand_rocks_02_arm_1k.jpg",
});
</script>

<template>
  <TresMesh
    receive-shadow
    :rotation="[-Math.PI * 0.5, 0, 0]"
    :position="[0, 0, 0]"
  >
    <TresPlaneGeometry :args="[20, 20]" />
    <TresMeshStandardMaterial
      v-bind="floorTexture"
      color="#82DBC5"
      :roughness="0.5"
      :metalness="0.5"
    />
  </TresMesh>
</template>
