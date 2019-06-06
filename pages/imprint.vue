<template>
  <div class="container">
    This my imprint

    {{ imprintData.headline }}

    <prismic-rich-text :field="imprintData.headline" />

  </div>
</template>

<script>
import Prismic from 'prismic-javascript'
import PrismicConfig from '~/prismic.config.js'

export default {
  name: 'Imprint',
  async asyncData({ context, error, req }) {
    try {
      const api = await Prismic.getApi(PrismicConfig.apiEndpoint, { req })

      const imprint = await api.query(
        Prismic.Predicates.at('document.type', 'imprint')
      )

      return {
        imprintData: imprint.results[0].data
      }
    } catch (e) {
      error({ statusCode: 404, message: 'Page not found' })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
