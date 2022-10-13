<script>
export default {
  data() {
    return {
      isHide: true,
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
</style>
