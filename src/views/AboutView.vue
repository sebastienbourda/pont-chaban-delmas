<script setup>
  import Footer from '../components/Footer.vue';
</script>

<template>
  <div class="about">
    <p>This website let you know if the bridge Jacques Chaban Delmas will
    be closed or not during the day.</p>
    <p>It use <a href="https://opendata.bordeaux-metropole.fr/pages/accueil/" target="_blank">Bordeaux Open Data</a> to find informations.</p>
    <p>It was created by <a href="">Sebastien Bourda</a>, Freelance Creative Developer based in Bordeaux, France.</p>
  </div>
  <Footer></Footer>
</template>

<style>
  .about {
    max-width: 90%;
  }
  p {
    font-size: 3rem;
  }
  a:hover {
    border-bottom: 2px solid;
  }
</style>
