<script>
export default {
  data() {
    return {
      isHide: true
    }
  },
  created() {
    this.animeFooter()
  },
  methods: {
    animeFooter() {
      // this.isActive = false
      setTimeout(() => {
        this.isHide = false
      }, 1200)
    }
  }
}
</script>

<template>
  <footer :class="{ 'footer-hide': isHide }">
    <h5>© Sebastien Bourda - 2022</h5>
    <ul class="menu">
      <li>
        <a href="mailto:sebastienbourda@icloud.com">Mail</a>
      </li>
      <li>
        <a href="www.linkedin.com/in/sebastien-bourda
" target="_blank">LinkedIn</a>
      </li>
      <li>
        <a href="/">twitter</a>
      </li>
      <li>
        <a href="https://github.com/sebastienbourda/pont-chaban-delmas" target="_blank">github</a>
      </li>
    </ul>
  </footer>
</template>

<style>
  footer {
    transition: all 600ms cubic-bezier(0.175, 0.885, 0.32, 1.275);
    min-height: 100px;
    justify-content: space-between;
  }
  .footer-hide {
    transform: translateY(120%);
  }
  @media (max-width: 800px) {
    footer {
      flex-direction: column;
      gap: 20px;
    }
  }
</style>
