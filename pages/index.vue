<template>
  <main>
    <div class="container">
      <div class="news">
        <div class="news__item" v-for="(item, index) in news" :key="index">
          <img v-if="item.image === ''" src="../assets/img/logo.png" class="news__item-img" alt="logo">
          <img v-else class="news__item-img" :src="item.image" alt="image">
          <div class="news__item-text">
            <small class="news__item-date">{{ reformDate(item.datePublish) }}</small>
            <a class="news__item-link" href="#!" @click.prevent="openNewsItem(item.slug)">
              <h1 class="news__item-title" :title="item.title">{{ validTitle(item.title) }}</h1>
            </a>
            <p class="news__item-description">{{ item.shortText }}</p>
          </div>
        </div>
      </div>
      <a href="#!" v-on:click="showMore()" class="news__item-btn">Показать ещё</a>
    </div>
  </main>
</template>
<script>
export default {
  data: () => ({
    title: 'Новости',
    news: [],
    page: 1,
  }),
  async asyncData({$axios}) {
    const news = await $axios.$get('https://domotekhnika.ru/api/v1/news?page=1').then((response) => {
      return response.data.news
    })
    return {news}
  },
  methods: {
    reformDate(datePublish) {
      return new Date(datePublish).toLocaleString('ru', {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
      })
    },
    validTitle(title) {
      if (title.length >= 29) {
        return `${title.substring(0, 37)}...`
      } else {
        return title
      }
    },
    showMore() {
      this.page++
      const news = this.$axios.$get(`https://domotekhnika.ru/api/v1/news?page=${this.page}`).then((response) => {
        [...response.data.news].forEach(item => {
          this.news.push(item)
        })
        return {news}
      })
    },
    openNewsItem(slug) {
        this.$router.push('/news/' + slug)
    }
  }
}
</script>

<style lang="scss">
.news {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 32px 40px;
  margin-bottom: 32px;

  &__item {
    display: flex;
    max-width: 509px;
    width: max-content;
  }

  &__item-date {
    color: rgba(0, 0, 0, 0.5);
    font-size: 13px;
    line-height: 140%;
    margin-bottom: 7px;
  }

  &__item-img {
    width: 200px;
    height: 200px;
    border-radius: 10px;
  }

  &__item-text {
    margin-left: 16px;
  }

  &__item-title {
    margin: 0 0 5px 0;
    font-size: 20px;
    font-weight: 400;
    line-height: 22px;
    letter-spacing: 0.15px;
  }

  &__item-link {
    text-decoration: none;
    color: #1D5AB6;
  }

  &__iitem-description {
    font-size: 16px;
    line-height: 140%;
    color: rgba(0, 0, 0, 0.8);
  }

  &__item-btn {
    background: #FFFFFF;
    padding: 12px 24px;
    border: 1px solid #CCCCCC;
    box-sizing: border-box;
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    transition: .5s;
    letter-spacing: 0.15px;
    color: rgba(0, 0, 0, 0.5);
    text-decoration: none;
    margin: 0 auto;
    display: block;
    width: max-content;
    font-family: Arial, serif;
    font-size: 20px;

    &:hover {
      background: #f6f6f6;
      color: rgba(0, 0, 0, 0.75);
      box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.25);
    }

    &:active {
      background: #c8c8c8;
      color: rgba(0, 0, 0, 1);
      box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.5);
    }
  }

  @media (max-width: 1200px) {
    grid-template-columns: none;
    width: fit-content;
    margin: 0 auto;
    padding-bottom: 32px;

    &__item {
      display: flex;
      max-width: none;
      width: auto;
    }
  }

  @media (max-width: 430px) {
    &__item {
      flex-direction: column-reverse;
      padding-bottom: 30px;
      border-bottom: 1px solid #ef6023;
    }

    &__item-img {
      margin: 0 auto;
    }

    &__item-description {
      margin-bottom: 1rem;
    }
  }
}
</style>
