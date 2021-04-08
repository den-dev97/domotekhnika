<template>
  <main class="news-item">
    <div class="container">
      <h1 class="news-item__title" :title="item.title">{{ item.title }}</h1>
      <img v-if="item.image === ''" src="../../assets/img/logo.png" class="news-item__img" alt="logo">
      <img v-else class="news-item__img" :src="item.image" alt="image">
      <p class="news-item__text" v-html="item.text">{{ item.text }}</p>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({$axios, params}) {
    const item = await $axios.$get(`https://domotekhnika.ru/api/v1/news/${params.slug}`).then((response) => {
      return response.data.news
    })
    return {item}
  },
}
</script>

<style scoped lang="scss">
.news-item {
  &__title {
    font-size: 28px;
    line-height: 140%;
    color: rgba(0, 0, 0, 0.8);
    margin-bottom: 11px;
  }

  &__img {
    width: 284px;
    height: 284px;
    border-radius: 10px;
    margin: 0 16px 16px 0;
    float: left;
  }

  &__text {
    font-family: Arial;
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 22px;
    letter-spacing: 0px;
    text-align: left;
  }
}
</style>
