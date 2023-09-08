<script>
// import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  // components: {
  //   HelloWorld,
  // },
};
</script>
<!-- <template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Welcome to Your Vue.js App" />
</template> -->

<script setup>
import { ref, computed } from "vue";
import Home from "./components/HelloWorld.vue";
import About from "./components/About.vue";
import NotFound from "./NotFound.vue";

const routes = {
  "/": Home,
  "/about": About,
};

const currentPath = ref(window.location.hash);

window.addEventListener("hashchange", () => {
  currentPath.value = window.location.hash;
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || "/"] || NotFound;
});
</script>

<template>
  <div class="nav-container">
    <a href="#/">Home</a> | <a href="#/about">About</a> |
    <a href="#/non-existent-path">Broken Link</a>
  </div>
  <div class="content-container">
    <component :is="currentView" />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.nav-container {
  background: beige;
  padding: 20px;
}
.content-container {
  margin-top: 20px;
}
</style>
