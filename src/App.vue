<script setup>
import { defineAsyncComponent } from "@vue/runtime-core"
import Splashscreen from "./components/splashscreen.vue";


const Home= defineAsyncComponent(()=>{
  return new Promise((resolve)=>{
    setTimeout(()=>{
      resolve(import("./components/Home.vue"))
    }, 2500);
  })
})
</script>

<template>
  <Suspense>
    <template #default>
      <Home />
    </template>
    <template #fallback>
      <Splashscreen />
    </template>
  </Suspense>
</template>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}
* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>