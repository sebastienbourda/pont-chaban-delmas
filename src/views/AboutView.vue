<script setup>
  import Footer from '../components/Footer.vue';
</script>

<template>
  <div class="about">
    <p>This website let you know if the bridge Jacques Chaban Delmas will
    be closed or not during the day.</p>
    <p>It uses <a href="https://opendata.bordeaux-metropole.fr/pages/accueil/" target="_blank">Bordeaux Open Data</a> to find informations.</p>
    <p>It has been created by Sebastien Bourda, Creative Developer based in Bordeaux, France.</p>
    <p>If you like the website, you can offer him a coffee <a href="https://www.buymeacoffee.com/778gnfcf9tx" target="_blank">there</a>.</p>
  </div>
  <Footer></Footer>
</template>

<style>
  .about {
    max-width: 960px;
    position: relative;
  }
  p {
    font-size: 2.5rem;
    margin: 2rem 0;
    line-height: 4rem;
  }
  .sign {
    position: absolute;
  }
  @media (max-width: 800px) {
    p {
      font-size: 1rem;
      margin: 0.8rem 0;
      line-height: 2rem;
    }
  }
</style>
