<template>
  <footer class="footer">
    <h1 class="footer__title">{{ title }}</h1>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      title: 'Footer'
    }
  }
}
</script>

<style scoped>
  .footer {
    min-height: 115px;
    display: flex;
    justify-content: center;
    vertical-align: center;
    margin-top: 32px;
    background-color: #ef6023;
    position: relative;
    width: 100%;
    bottom:0;
  }
</style>
