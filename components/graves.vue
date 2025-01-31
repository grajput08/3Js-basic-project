<script setup>
import { reactive } from "vue";
import { BoxGeometry, MeshStandardMaterial } from "three";
import { useTexture } from "@tresjs/core";

const configureTexture = async (pathConfig) => {
  const texture = await useTexture(pathConfig);
  return texture;
};

const wallTexture = await configureTexture({
  map: "/haunted-house/wall/castle_brick_broken_06_diff_1k.jpg",
  normalMap: "/haunted-house/wall/castle_brick_broken_06_nor_gl_1k.jpg",
  aoMap: "/haunted-house/wall/castle_brick_broken_06_arm_1k.jpg",
});

const graveGeometry = new BoxGeometry(0.6, 0.8, 0.1);
const graveMaterial = new MeshStandardMaterial({
  ...wallTexture,
  color: "#727272",
});

const generateGraves = (count) => {
  return Array.from({ length: count }, () => {
    const angle = Math.random() * Math.PI * 2;
    const radius = 3 + Math.random() * 6;
    const x = Math.cos(angle) * radius;
    const z = Math.sin(angle) * radius;
    return {
      position: [x, 0.3, z],
      rotation: [(Math.random() - 0.5) * 0.4, (Math.random() - 0.5) * 0.4, 0],
    };
  });
};

const graves = reactive(generateGraves(50));
</script>

<template>
  <TresGroup>
    <TresMesh
      v-for="(grave, index) in graves"
      :key="index"
      :position="[grave.position[0], grave.position[1], grave.position[2]]"
      :rotation="[grave.rotation[0], grave.rotation[1], grave.rotation[2]]"
      :geometry="graveGeometry"
      :material="graveMaterial"
    />
  </TresGroup>
</template>
