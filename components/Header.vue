<template>
  <header class="header">
    <h1 class="header__title">{{ title }}</h1>
  </header>
</template>

<script>
export default {
  data() {
    return {
      title: 'Header'
    }
  }
}
</script>

<style scoped>
  .header {
    min-height: 115px;
    background-color: #ef6023;
    display: flex;
    justify-content: center;
    vertical-align: center;
    margin-bottom: 32px;
  }
</style>
