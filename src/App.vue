<script setup>
import NavBar from "./components/NavBar.vue";
import { useRoute } from "vue-router";
</script>
<template>
  <NavBar />
  <RouterView />
</template>
