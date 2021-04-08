<template>
  <div>
    <Header/>
    <Nuxt/>
    <Footer/>
  </div>
</template>

<script>
import Header from "@/components/Header";
import Footer from "@/components/Footer";
export default {
  comments: {
    Header,
    Footer,
  }
}
</script>

<style lang="scss">
html {
  font-family: 'Source Sans Pro',
  -apple-system,
  BlinkMacSystemFont,
  'Segoe UI',
  Roboto,
  'Helvetica Neue',
  Arial,
  sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

main {
  min-height: calc(84vh - 115px);
}

header, footer, section, .container {
  padding: 0 15px;

  @media (min-width: 575.98px) {
    padding: 0 calc(50vw - 270px);
  }

  @media (min-width: 767.98px) {
    padding: 0 calc(50vw - 360px);
  }

  @media (min-width: 991.98px) {
    padding: 0 calc(50vw - 480px);
  }

  @media (min-width: 1199.98px) {
    padding: 0 calc(50vw - 590px);
  }
}
</style>
