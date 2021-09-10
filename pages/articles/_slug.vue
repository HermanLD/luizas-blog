<template>
  <div class="article-wrap">
    <header class="article-header">
      <h1 class="title">
        <!-- TODO: Create a filter for date -->
        <span class="title-date">{{ article.publishDate | formatDate }}</span
        >{{ article.title }}
      </h1>
      <figure class="image">
        <img
          class="image-core"
          :src="article.postImage"
          :alt="article.postImageAlt"
        />
      </figure>
    </header>
    <article class="article-post">
      <nuxt-content :document="article" />
    </article>
    <p class="article-attribute">
      Article image credits -
      <a :href="article.imageCreditLink">{{ article.imageCreditName }}</a>
    </p>
  </div>
</template>

<script>
export default {
  filters: {
    formatDate(rawDate) {
      const date = new Date(rawDate)
      const dateStr = date.toDateString()
      const dateArr = dateStr.split(' ')
      return `${dateArr[2]} ${dateArr[1]} ${dateArr[3]} `
    },
  },
  layout: 'article',
  async asyncData({ $content, params }) {
    const article = await $content('articles', params.slug).fetch()

    return {
      article,
    }
  },
  head() {
    return {
      title: this.article.title,
      meta: [
        { hid: 'og:title', property: 'og:title', content: this.article.title },
        {
          hid: 'og:description',
          property: 'og:description',
          content: this.article.description,
        },
        {
          hid: 'og:image',
          property: 'og:image',
          content: this.article.postImage,
        },
      ],
    }
  },
}
</script>

<style>
.article-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: var(--clr-light);
}

.article-header {
  padding: 6.6rem 0 0;
  text-align: center;
  max-width: 115.2rem;
  background-color: white;
}

.article-header .title {
  font-size: 3.2rem;
  line-height: 1.3;
  margin-bottom: 3rem;
}

.article-header .title-date {
  display: block;
  margin-bottom: 0.8rem;
  color: var(--clr-gray);
  font-size: 2.4rem;
  font-family: var(--ff-body);
  font-weight: var(--fw-light);
}

.article-header .image {
  border-radius: 5px;
  overflow: hidden;
}

.article-post {
  position: relative;
  top: -6.5rem;
  background-color: hsl(0, 0%, 100%);
  width: 94%;
  max-width: 97.6rem;
  padding: var(--article-post-lag-pad, 3.6rem 3rem);
  font-size: 1.6rem;
  letter-spacing: 1px;
  line-height: 1.4;

  box-shadow: 2px -1px 7px 1px var(--clr-dark-o);
}

.article-post .nuxt-content p {
  line-height: 1.7;
  margin-bottom: 1.2rem;
}
.article-post .nuxt-content blockquote {
  padding: 1.6rem 1.2rem;
  border-left: 10px solid var(--clr-primary-2);
  background-color: var(--clr-gray);
  font-size: 1.8rem;
  color: hsl(0, 0%, 100%);
}

@media screen and (min-width: 700px) {
  .article-post {
    --article-post-lag-pad: 9.6rem 9.6rem;
  }
}
</style>
