<script setup lang="ts">
import { OrbitControls } from "@tresjs/cientos";
import { TresCanvas } from "@tresjs/core";
import House from "../components/haunted-house/house.vue";
</script>

<template>
  <TresCanvas window-size clear-color="#262837" shadows>
    <TresPerspectiveCamera :position="[4, 2, 5]" />
    <TresFog :args="['#262837', 1, 15]" />
    <OrbitControls />
    <Suspense>
      <House />
    </Suspense>
  </TresCanvas>
</template>
