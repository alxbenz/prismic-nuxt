
<template>
  <section>
    <div class="image">
      <picture>
        <source :srcset="`${post.data.image.small.url} 1200w, ${post.data.image.url} 1600w`" media="(min-width: 600px)">
        <img :src="`${post.data.image.mobile.url}`" :alt="post.data.image.alt">
      </picture>
    </div>
    <div class="container">
      <h1>{{ post.data.headline }}</h1>

      <prismic-rich-text :field="post.data.content_richtext" />

      <template v-if="post.data.screens">
        <p v-for="screen in post.data.screens" :key="screen.screen.url">
          <img class="screen" :src="screen.screen.url" :alt="screen.screen.alt">
        </p>
      </template>

      <nav class="navigate">
        <nuxt-link v-if="prev" :to="`/posts/${prev.uid}`" class="prev">
          &lt;-- {{ prev.data.headline }}
        </nuxt-link>

        <nuxt-link v-if="next" :to="`/posts/${next.uid}`" class="next">
          {{ next.data.headline }} --&gt;
        </nuxt-link>
      </nav>
    </div>
  </section>
</template>

<router>
    path: /posts/:title
</router>

<script>
import Prismic from 'prismic-javascript'
import PrismicConfig from '~/prismic.config.js'

export default {
  transition: {
    name: 'page',
    mode: 'out-in'
  },
  name: 'Post',
  async asyncData({ params, error, req }) {
    try {
      const api = await Prismic.getApi(PrismicConfig.apiEndpoint, { req })

      const posts = await api.query(
        Prismic.Predicates.at('document.type', 'post'),
        { orderings: '[my.post.squence]' }
      )

      let index = null

      const currentPost = posts.results.filter((post, i) => {
        if (post.uid === params.title) {
          index = i
          return true
        }
      })[0]

      const previousPost = posts.results[index - 1]
      const nextPost = posts.results[index + 1]

      return {
        prev: previousPost,
        post: currentPost,
        next: nextPost
      }
    } catch (e) {
      error({ statusCode: 404, message: 'Page not found' })
    }
  }
}
</script>

<style lang="scss">
.navigate {
  width: 100%;
  max-width: 500px;
  margin-top: 50px;
  display: flex;
  justify-content: space-between;
}

.screen {
  max-width: 100%;
}
</style>
