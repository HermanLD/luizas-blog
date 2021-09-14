<template>
  <div id="front-page">
    <header
      class="front-page-header"
      :style="{ backgroundImage: `url(${home.header_image})` }"
    >
      <h1 class="front-page-title">
        {{ home.title }}<span class="sub-text">{{ home.subtext }}</span>
      </h1>
    </header>
    <section class="front-page-articles">
      <ul class="grid">
        <!-- FIRST GRID ITEM -->
        <li class="about-me">
          <div>
            <img class="about-me-img" :src="home.about_me_image" />
          </div>
          <div class="about-me-content">
            <h2 class="header">About Me</h2>
            <p>{{ home.about_me }}</p>
          </div>
        </li>
        <!-- ARTICLE GRID -->
        <li
          v-for="article in articles"
          :key="article.slug"
          class="article-item"
        >
          <nuxt-link class="article-item-card" :to="article.path">
            <div>
              <img
                class="article-item-img"
                :src="article.image"
                :alt="article.image_description"
              />
            </div>
            <div class="article-item-content">
              <ul class="tags">
                <li v-for="tag in article.tags" :key="tag" class="tag">
                  {{ tag }}
                </li>
              </ul>
              <h3 class="title">{{ article.title }}</h3>
              <p>{{ article.description }}</p>
            </div>
          </nuxt-link>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const home = await $content('home').fetch()

    const articles = await $content('articles').fetch()

    return { home, articles }
  },
  data() {
    return { title: 'Luiza Benisano - Blog' }
  },
  head() {
    return {
      title: this.title,
      meta: [{ hid: 'og:title', property: 'og:title', content: this.title }],
    }
  },
}
</script>

<style>
.front-page-header {
  position: relative;
  width: 100%;
  height: 60vh;
  padding: 7.5rem 0 0 0;
  text-align: center;

  background-size: cover;
  background-repeat: no-repeat;
}

.front-page-header::after {
  content: '';
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  background-image: radial-gradient(circle, transparent 55%, black 85%);
}

.front-page-title {
  color: var(--clr-light);
  font-size: 6.2rem;
}

.front-page-title > .sub-text {
  display: block;
  margin-top: 1.4rem;
  font-size: 3.2rem;
}

.front-page-articles {
  padding: 0 1.6rem;
}

.front-page-articles > .grid {
  position: relative;
  top: -8.6rem;
  display: grid;
  grid-template-columns: repeat(var(--grid-col-num, 1), 1fr);
  gap: 4.8rem;

  margin: 0 auto 4.8rem;
  width: 100%;
  max-width: 93rem;
}

.front-page-articles .about-me,
.front-page-articles .article-item {
  border-radius: 5px;
  background-color: var(--clr-light);
  overflow: hidden;

  /* .front-page-articles .article-item:hover */
  transition: 0.3s ease-out;
}

.front-page-articles .article-item:hover {
  transform: scale(1.05);
}

.front-page-articles .about-me,
.article-item-card {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(25rem, 1fr));

  grid-column: span var(--grid-col-num, 1) / auto;
}

.front-page-articles .about-me-img,
.front-page-articles .article-item-img {
  width: 100%;
  object-fit: fill;
}

.front-page-articles .about-me-content {
  padding: 4.8rem 2.4rem 4.5rem;
  font-size: 1.6rem;
  line-height: 1.3;
  letter-spacing: 1px;
}

.front-page-articles .article-item-content {
  padding: 3.2rem 1.6rem;
  font-size: 1.5rem;
  line-height: 1.3;
}

.front-page-articles .article-item-content .tags {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
  color: var(--clr-gray);
}

.front-page-articles .article-item-content .tag {
  margin-right: 1.2rem;
}

.front-page-articles .article-item-content .title {
  font-size: 2rem;
  margin-bottom: 1.8rem;
}

.front-page-articles .about-me-content .header {
  font-size: 2.4rem;
  margin-bottom: 2rem;
}

.front-page-articles .article-item:nth-child(1),
.front-page-articles .article-item:nth-child(2),
.front-page-articles .article-item:nth-child(3),
.front-page-articles .article-item:nth-child(8),
.front-page-articles .article-item:nth-child(9),
.front-page-articles .article-item:nth-child(10),
.front-page-articles .article-item:nth-child(15),
.front-page-articles .article-item:nth-child(16),
.front-page-articles .article-item:nth-child(17),
.front-page-articles .article-item:nth-child(7),
.front-page-articles .article-item:nth-child(14),
.front-page-articles .article-item:nth-child(21) {
  grid-column: span var(--article-third, 1) / auto;
}

.front-page-articles .article-item:nth-child(4),
.front-page-articles .article-item:nth-child(5),
.front-page-articles .article-item:nth-child(11),
.front-page-articles .article-item:nth-child(12),
.front-page-articles .article-item:nth-child(18),
.front-page-articles .article-item:nth-child(19) {
  grid-column: span var(--article-half, 1) / auto;
}

.front-page-articles .article-item:nth-child(6),
.front-page-articles .article-item:nth-child(13),
.front-page-articles .article-item:nth-child(20) {
  grid-column: span var(--article-large, 1) / auto;
}
@media screen and (min-width: 875px) {
  .front-page-articles {
    --grid-col-num: 6;
    --article-third: 2;
    --article-half: 3;
    --article-large: 4;
  }
}
</style>
