<script setup>
import { reactive } from "vue";

const bushes = reactive([
  { scale: [0.5, 0.5, 0.5], position: [0.8, 0.2, 2.2] },
  { scale: [0.25, 0.25, 0.25], position: [1.4, 0.1, 2.1] },
  { scale: [0.4, 0.4, 0.4], position: [-0.8, 0.1, 2.2] },
  { scale: [0.15, 0.15, 0.15], position: [-1, 0.05, 2.6] },
]);
</script>

<template>
  <TresMesh
    v-for="(bush, index) in bushes"
    :key="index"
    :position="[bush.position[0], bush.position[1], bush.position[2]]"
    :scale="[bush.scale[0], bush.scale[1], bush.scale[2]]"
  >
    <TresSphereGeometry :args="[1, 16, 16]" />
    <TresMeshStandardMaterial color="#89c854" />
  </TresMesh>
</template>
