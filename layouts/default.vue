<template>
  <div>
    <hc-frame>
      <div class="container" id="main">
        <hc-verification-banner/>
        <nuxt/>
      </div>
      <hc-footer/>
    </hc-frame>
  </div>
</template>

<script>
  import HcFooter from '~/components/layout/Footer.vue'
  import HcFrame from '~/components/layout/Frame.vue'
  import HcVerificationBanner from '~/components/layout/VerificationBanner.vue'

  export default {
    components: {
      HcFooter,
      HcFrame,
      HcVerificationBanner
    },
    head () {
      return {
        htmlAttrs: {
          lang: this.$i18n.locale()
        }
      }
    }
  }
</script>

<style scoped lang="scss">
  #main {
    margin-bottom: 15em !important;
  }
</style>
