<template>
  <section>
    <div class="container">
      <div>
        title: {{ getDemo.data.title }}
      </div>
      <div>
        richtext: <prismic-rich-text :field="getDemo.data.richtext" />
      </div>
      <div>
        selected option: {{ getDemo.data.dropdown }}
      </div>
      <div>
        selected date: {{ getDemo.data.date }}
      </div>
      <div>
        some numbers: <span v-for="numberObject in getDemo.data.group" :key="numberObject.number">{{ numberObject.number }}</span>
      </div>

      <button @click="showPre = !showPre">
        Toggle JSON
      </button>
      <pre v-show="showPre">
        {{ fullJSON }}
      </pre>
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
  name: 'Demo',
  data() {
    return {
      showPre: false
    }
  },
  async asyncData({ params, error, req }) {
    try {
      const api = await Prismic.getApi(PrismicConfig.apiEndpoint, { req })

      const demo = await api.query(
        Prismic.Predicates.at('document.type', 'demo'),
        { orderings: '[document.first_publication_date]' }
      )

      return {
        fullJSON: demo,
        getDemo: demo.results[0]
      }
    } catch (e) {
      error({ statusCode: 404, message: 'Page not found' })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
