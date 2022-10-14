<script>
export default {
  data() {
    return {
      isHide: true,
      isActive: false,
      currentPage: ""
    }
  },
  mounted() {
    this.animeHeader(),
    this.currentPage = window.location.pathname,
    this.displayCurrentPage()
  },
  methods: {
    animeHeader() {
      // this.isActive = false
      setTimeout(() => {
        this.isHide = false
      }, 1600)
    },
    displayCurrentPage() {
      console.log(this.currentPage)
    }
  }
}
</script>

<template>
  <header :class="{ 'header-hide': isHide }" >
    <h5>PONT CHABAN DELMAS</h5>
    <ul class="menu">
      <li>
        <RouterLink to="/">Home</RouterLink>
      </li>
      <li>
        <RouterLink to="/about">About</RouterLink>
      </li>
    </ul>
  </header>
</template>

<style>
  header {
    transition: all 600ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
  }
  .header-hide {
    transform: translatey(-200%);
  }
  .router-link-active {
    padding-bottom: 5px;
  }
  .router-link-active::after {
    content: '';
    border-bottom: 3px solid var(--vt-c-red);
    width: 20px;
    display: block;
  }
  .menu a:not(.router-link-active)::after{
    content: '';
    border-bottom: 3px solid var(--vt-c-red);
    opacity: 0;
    width: 20px;
    display: block;
    transition: all 300ms ease-in-out;
  }
  .menu a:not(.router-link-active):hover::after {
    content: '';
    border-bottom: 3px solid var(--vt-c-red);
    width: 100%;
    display: block;
    opacity: 1;
  }
</style>
