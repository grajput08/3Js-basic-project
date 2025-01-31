<script setup lang="ts">
import { OrbitControls } from "@tresjs/cientos";
import { TresCanvas } from "@tresjs/core";
</script>

<template>
  <TresCanvas window-size clear-color="#262837" shadows>
    <TresPerspectiveCamera :position="[4, 2, 5]" />
    <TresFog :args="['#262837', 1, 20]" />
    <OrbitControls />
    <Suspense>
      <House />
    </Suspense>
    <Suspense>
      <Floor />
    </Suspense>
    <Suspense>
      <Bushes />
    </Suspense>
    <Suspense>
      <Graves />
    </Suspense>
    <Suspense>
      <Ghost />
    </Suspense>
  </TresCanvas>
</template>
