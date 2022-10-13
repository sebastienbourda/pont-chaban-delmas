<script>
  export default{
    data () {
      return{
        isLoaded: false
      }
    },
    mounted() {
      setTimeout(() => {
        this.isLoaded = true;
      }, 1000);
    }
  }
</script>

<template>
  <div class="loader" v-if="!isLoaded">
    <div class="dots">
      <span class="dot"></span>
      <span class="dot"></span>
      <span class="dot"></span>
    </div>
  </div>
</template>

<style>
  .loader{
    height: 100vh;
    width: 100%;
    background-color: var(--vt-c-light-red);
    position: absolute;
    top: 0;
    z-index: 2;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
  }

  .dots{
    display: flex;
    align-items: center;
    height: 100%;
    gap: 10px;
  }

  .dot{
    height: 30px;
    width: 30px;
    display: block;
    border-radius: 30px;
    background-color: var(--vt-c-red);
    animation-name: opacity;
    animation-duration: 1.2s;
    animation-iteration-count: infinite;
    animation-timing-function:  ease-in-out;
  }

  .dot:nth-of-type(2){
    animation-delay: 0.2s;
  }

  .dot:nth-of-type(3){
    animation-delay: 0.6s;
  }

  @keyframes opacity {
    30%{
      opacity: 0.3;
      transform: translateY(15px);
    }
  }
</style>
