<script setup lang="ts">
import { GLTFModel, OrbitControls, Environment } from "@tresjs/cientos";
import { TresCanvas } from "@tresjs/core";
</script>

<template>
  <div class="scene-container">
    <TresCanvas>
      <TresPerspectiveCamera :position="[3, 2, 5]" />
      <OrbitControls />
      <Suspense>
        <GLTFModel :path="`/models/DamagedHelmet.glb`" />
      </Suspense>
      <Suspense>
        <Environment background files="/environmentMaps/2k.hdr" />
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
