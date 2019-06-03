<template>
  <div>
    <page-header />
    <nuxt class="nuxt-content" />
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
