<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Header from './components/Header.vue';
import Loader from './components/Loader.vue';
import Footer from './components/Footer.vue';
</script>

<template>
  <Loader></Loader>
  <Header></Header>
  <RouterView />
</template>

<style scoped>
</style>
