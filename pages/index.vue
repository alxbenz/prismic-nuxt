<template>
  <section>
    <div class="image">
      <picture>
        <source :srcset="`${homepageData.image.small.url} 1200w, ${homepageData.image.url} 1600w`" media="(min-width: 600px)">
        <img :src="`${homepageData.image.mobile.url}`" :alt="homepageData.image.alt">
      </picture>
    </div>
    <div class="container">
      <h1>
        {{ homepageData.title }}
      </h1>
      <h3>Contents</h3>
      <ol>
        <li v-for="post in posts" :key="post.id">
          <nuxt-link :to="`/posts/${post.uid}`">
            {{ post.data.headline }}
          </nuxt-link>
        </li>
      </ol>
    </div>
  </section>
</template>

<script>
import Prismic from 'prismic-javascript'
import PrismicConfig from '~/prismic.config.js'

export default {
  transition: {
    name: 'page',
    mode: 'out-in'
  },
  name: 'Index',
  async asyncData({ context, error, req }) {
    try {
      const api = await Prismic.getApi(PrismicConfig.apiEndpoint, { req })

      const homepage = await api.query(
        Prismic.Predicates.at('document.type', 'homepage')
      )
      const posts = await api.query(
        Prismic.Predicates.at('document.type', 'post'),
        { orderings: '[document.first_publication_date]' }
      )

      return {
        homepageData: homepage.results[0].data,
        posts: posts.results
      }
    } catch (e) {
      error({ statusCode: 404, message: 'Page not found' })
    }
  }
}
</script>
