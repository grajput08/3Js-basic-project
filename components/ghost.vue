<script setup>
import { useRenderLoop } from "@tresjs/core";
import { shallowRef } from "vue";

// References for the ghosts
const ghost1 = shallowRef(null);
const ghost2 = shallowRef(null);
const ghost3 = shallowRef(null);

// Constants for ghost movement properties
const ghostConfigs = [
  { speed: 0.5, radius: 4, yMultiplier: 3 },
  { speed: -0.32, radius: 5, yMultiplier: [4, 2.5] },
  {
    speed: -0.18,
    radius: 7,
    yMultiplier: [4, 2.5],
    oscillationSpeed: [0.32, 0.5],
  },
];

// Render loop for ghost movement
const { onLoop } = useRenderLoop();
onLoop(({ elapsed }) => {
  if (ghost1.value && ghost2.value && ghost3.value) {
    const [ghost1Config, ghost2Config, ghost3Config] = ghostConfigs;

    const ghost1Angle = elapsed * ghost1Config.speed;
    ghost1.value.position.x = Math.cos(ghost1Angle) * ghost1Config.radius;
    ghost1.value.position.z = Math.sin(ghost1Angle) * ghost1Config.radius;
    ghost1.value.position.y = Math.sin(
      elapsed * Number(ghost1Config.yMultiplier)
    );

    const ghost2Angle = elapsed * ghost2Config.speed;
    ghost2.value.position.x = Math.cos(ghost2Angle) * ghost2Config.radius;
    ghost2.value.position.z = Math.sin(ghost2Angle) * ghost2Config.radius;
    ghost2.value.position.y =
      Math.sin(elapsed * ghost2Config.yMultiplier[0]) +
      Math.sin(elapsed * ghost2Config.yMultiplier[1]);

    const ghost3Angle = elapsed * ghost3Config.speed;
    ghost3.value.position.x =
      Math.cos(ghost3Angle) *
      (ghost3Config.radius +
        Math.sin(elapsed * ghost3Config.oscillationSpeed[0]));
    ghost3.value.position.z =
      Math.sin(ghost3Angle) *
      (ghost3Config.radius +
        Math.sin(elapsed * ghost3Config.oscillationSpeed[1]));
    ghost3.value.position.y =
      Math.sin(elapsed * ghost3Config.yMultiplier[0]) +
      Math.sin(elapsed * ghost3Config.yMultiplier[1]);
  }
});
</script>

<template>
  <!-- Ambient light for overall scene illumination -->
  <TresAmbientLight color="#b9d5ff" :intensity="0.8" />

  <!-- Point lights for ghost effects -->
  <TresPointLight ref="ghost1" :args="['#ff00ff', 3, 3]" cast-shadow />
  <TresPointLight ref="ghost2" :args="['#00ffff', 3, 3]" cast-shadow />
  <TresPointLight ref="ghost3" :args="['#ff7800', 3, 3]" cast-shadow />
</template>
