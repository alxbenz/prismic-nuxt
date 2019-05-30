<template>
  <div>
    <page-header />
    <nuxt class="nuxt-content" />
    <nuxt-link :to="{path: '/demo'}" class="btn-demo">
      Demo Content
    </nuxt-link>
    <page-footer />
  </div>
</template>

<script>
import PageHeader from '@/components/PageHeader.vue'
import PageFooter from '@/components/PageFooter.vue'

export default {
  name: 'DefaultLayout',
  components: {
    PageHeader,
    PageFooter
  }
}
</script>
