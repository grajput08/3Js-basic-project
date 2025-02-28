<script setup lang="ts">
import { ref } from "vue";

const pages = [
  {
    title: "Basic Scene",
    description:
      "A basic 3D scene with interactive controls for shapes, colors, and camera positioning using TresJS and lil-gui.",
    path: "/basic",
  },
  {
    title: "Lights and Shadows",
    description: "A scene with lights and shadows using Three.js and Vue 3.",
    path: "/lights-shadows",
  },
  {
    title: "Haunted House",
    description:
      "A spooky 3D haunted house scene with atmospheric effects and interactive elements.",
    path: "/haunted-house",
  },
  {
    title: "Imported Model",
    description:
      "A composable that allows you to easily load glTF models into your TresJS scene.",
    path: "/imported-model",
  },
  {
    title: "Environment Mapping",
    description:
      "Demonstrates environment mapping using TresJS's useEnvironment composable for realistic reflections and lighting.",
    path: "/environment-map",
  },
];
</script>

<template>
  <div class="container">
    <div class="gradient-background"></div>

    <h1 class="title">TresJS Demo Project</h1>
    <p class="description">
      Explore different 3D scenes built with TresJS, Vue 3, and Three.js. Each
      demo showcases different capabilities and interactive features.
    </p>

    <div class="pages-grid">
      <div v-for="page in pages" :key="page.path" class="page-card">
        <NuxtLink :to="page.path" class="page-link" target="_blank">
          <h2>{{ page.title }}</h2>
          <p>{{ page.description }}</p>
          <span class="view-button">View Scene →</span>
        </NuxtLink>
      </div>
    </div>

    <footer class="footer">
      <a
        href="https://github.com/grajput08/3Js-basic-project"
        target="_blank"
        class="github-link"
      >
        <svg
          height="32"
          aria-hidden="true"
          viewBox="0 0 16 16"
          version="1.1"
          width="32"
        >
          <path
            fill-rule="evenodd"
            d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"
          ></path>
        </svg>
        View on GitHub
      </a>
    </footer>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap");

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: "Inter", sans-serif;
  position: relative;
  min-height: 100vh;
}

.gradient-background {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom right, #003543, #00283d, #001b2e);
  z-index: -1;
}

.title {
  font-size: 3.5rem;
  margin-bottom: 1rem;
  color: #fff;
  font-weight: 700;
  background: linear-gradient(to right, #42b883, #3fb27f);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

.description {
  font-size: 1.2rem;
  color: #e0e0e0;
  margin-bottom: 3rem;
  max-width: 800px;
  line-height: 1.6;
}

.pages-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.page-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 12px;
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.page-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
  border-color: rgba(66, 184, 131, 0.4);
}

.page-link {
  display: block;
  padding: 1.5rem;
  text-decoration: none;
  color: inherit;
}

.page-link h2 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
  color: #fff;
  font-weight: 600;
}

.page-link p {
  color: #e0e0e0;
  margin-bottom: 1rem;
  line-height: 1.5;
}

.view-button {
  display: inline-block;
  color: #42b883;
  font-weight: 500;
  transition: color 0.2s ease;
}

.view-button:hover {
  color: #3fb27f;
  text-decoration: none;
}

.footer {
  position: absolute;
  bottom: 2rem;
  left: 0;
  right: 0;
  text-align: center;
}

.github-link {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  color: #fff;
  text-decoration: none;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.1);
  transition: all 0.2s ease;
}

.github-link:hover {
  background: rgba(255, 255, 255, 0.2);
}

.github-link svg {
  fill: currentColor;
}
</style>
