<template>
  <BasePage>
    <div slot="readme" ref="readme" v-html="readme"></div>
    <div slot="example" ref="example">
      <!-- <word-cloud :value="cloudText"
                  :size="svgSize"
                  :rotate="seansRadius"
                  :immediate="true" /> -->
      <DemoComponent ref="demothing" />
    </div>
  </BasePage>
</template>

<script>
import readme from './readme.md'
import BasePage from '@/views/BasePage.vue'
export default {
  data() {
    return {
      readme,
      cloudText:   null,
      svgSize:     [1000, 1000],
      rotations:   [0, 360],
      seansRadius: () => (Math.random() > 0.5 ? 0 : (90 * Math.PI) / 180)
    }
  },
  components: {
    DemoComponent: () => import('./finished.vue'),
    BasePage
  },
  mounted() {
    this.$nextTick(() => {
      const rect = this.$refs.example.getBoundingClientRect()
      this.svgSize = [rect.width, rect.height]
      //   this.$data._words = _.words(this.$el.innerText)
      this.cloudText = this.$refs.readme.innerText
    })
  }
}
</script>
