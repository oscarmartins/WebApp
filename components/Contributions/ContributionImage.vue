<template>
    <hc-progressive-image
        v-if="src"
        class="teaser-image"
        :preview="getPlaceholder"
        :src="getCover"
        @click.native="imageModal"/>
</template>

<script>
  /**
   * TODO: we need to refactor this component for less complexity
   */
  export default {
    name: 'hc-contribution-image',
    props: {
      src: {
        type: [String, Object]
      },
      refresh: {
        type: [Number, String]
      }
    },
    data () {
      return {
        url: {
          cover: '',
          placeholder: '',
          zoom: ''
        }
      }
    },
    created () {
      try {
        this.url.cover = this.src.cover || this.src || null
        this.url.placeholder = this.src.coverPlaceholder || this.src || null
        this.url.zoom = this.src.zoom || this.src || null
      } catch (err) {}
    },
    watch: {
      src (src) {
        this.url.cover = src.cover || src || null
        this.url.placeholder = src.coverPlaceholder || src || null
        this.url.zoom = src.zoom || src || null
      }
    },
    computed: {
      getCover () {
        return this.url.cover || null
      },
      getPlaceholder () {
        return this.url.placeholder || null
      }
    },
    mounted () {
      // this is fixin an issue with the default avatar
      // while picking the name after regestration
      if (parseInt(this.refresh) > 0 && this.url.cover) {
        setTimeout(() => {
          // retry to load image
          this.url.cover = ''
          this.url.placeholder = ''
          this.url.zoom = ''
          this.$nextTick(() => {
            this.url.cover = this.src.cover || this.src || null
            this.url.placeholder = this.src.coverPlaceholder || this.src || null
            this.url.zoom = this.src.zoom || this.src || null
          }, 0)
        }, parseInt(this.refresh))
      }
    },
    methods: {
      imageModal () {
        this.$modal.open({
          content: `<p class="image">
                          <img src="${this.url.zoom}">
                      </p>`,
          animation: 'zoom-in'
        })
      }
    }
  }
</script>

<style scoped lang="scss">
    @import 'assets/styles/utilities';

    .teaser-image {
        margin: -3rem -1.5rem 1.5rem;
        cursor: zoom-in;
        // height: 300px;
        overflow: hidden;
    }

    /* .hc__imagecontainer {
        height: 300px;
        background-size: cover;
        background-position: top;
        // overflow: hidden;
        margin: -3rem -1.5rem 2.5rem -1.5rem !important;
        cursor: zoom-in;

        opacity: 0;
        transition: opacity 150ms ease-in-out;

        &.ready {
            opacity: 1;
        }

        @include mobile() {
            height: 60vw;
        }
        @include tablet-only() {
            height: 40vw;
        }
    } */
</style>
