
<template>
  <main
    class="homepage"
    aria-labelledby="main-title"
  >
    <header class="hero">
      <img
        v-if="data.heroImage"
        :src="$withBase(data.heroImage)"
        :alt="data.heroAlt || $title"
      >

      <div>
        <h1
          v-if="data.heroText !== null"
          id="main-title"
        >
          {{ data.heroText || $title }}
        </h1>

        <p
          v-if="data.tagline !== null"
          class="description"
        >
          {{ data.tagline || $description }}
        </p>
      </div>
    </header>

    <div
      v-if="data.features && data.features.length"
      class="features"
    >
      <div
        v-for="(feature, index) in data.features"
        :key="index"
        class="feature"
      >
        <h2>{{ feature.title }}</h2>
        <p>{{ feature.details }}</p>
        <NavLink
          v-if="feature.actionLink"
          class="action-button"
          :item="{ link: feature.actionLink, text: feature.actionText }"
        />
      </div>
    </div>

    <Content class="theme-default-content custom" />

    <div
      v-if="data.footer"
      class="footer"
    >
      {{ data.footer }}
    </div>
  </main>
</template>

<script>
// forked from https://github.com/vuejs/vuepress/blob/master/packages/%40vuepress/theme-default/components/Home.vue
import NavLink from '@theme/components/NavLink.vue'
import { toggleColorMode } from '../../themeSwitch'

export default {
  name: 'Home',

  components: {
    NavLink
  },

  computed: {
    data () {
      return this.$page.frontmatter
    },
    actionLink () {
      return {
        link: this.data.actionLink,
        text: this.data.actionText
      }
    },
    algolia () {
      return this.$themeLocaleConfig.algolia || this.$site.themeConfig.algolia || {}
    }
  },

  methods: {
    toggleColorMode
  }
}
</script>

<style lang="stylus">
.homepage
  max-width $homePageWidth
  margin 0px auto
  display block
  padding  1rem
  .hero
    padding 3rem 1rem
    display flex
    align-items center
    justify-content center
    position relative
    text-align center
    img
      max-width 100%
      max-height 150px
      min-height 60px
    h1
      margin 0 auto
      font-size 2.5rem
    .description
      font-size 1.25rem
      margin .5rem auto 0
      line-height 1.3
      color var(--zeus-secondary)
  h3
    color var(--zeus-secondary)
    font-weight var(--zeus-font-weight-normal)
  .action-button
    display inline-block
    font-size 1.2rem
    color #242930
    background-color var(--zeus-primary)
    padding 0.8rem 1.6rem
    border-radius 4px
    transition background-color .1s ease
    box-sizing border-box
    border-bottom 1px solid var(--zeus-body-border-medium)
    &:focus,
    &:hover
      background-color var(--zeus-primary-accent)
  .features
    margin-top 2.5rem
    margin-bottom 2.5rem
    display flex
    flex-wrap wrap
    justify-content center
  .feature
    flex 0 0 250px
    text-align center
    padding 2rem 1rem
    h2
      font-size 1.4rem
      font-weight var(--zeus-font-weight-normal)
      border-bottom none
      margin-top 0
      padding-bottom 0
      color var(--zeus-secondary)
    .action-button
      display inline-block
      width 250px
  .topics
    text-align center
    margin-bottom 4rem
    ul
      list-style none
      display flex
      flex-wrap wrap
      justify-content center
      padding 0
    li
      flex 0 0 282px
      text-align center
      padding 1rem
    a
      display flex
      align-items center
      justify-content center
      width 100%
      height 5.5em
      border 1px solid var(--zeus-body-border-medium)
      border-radius var(--zeus-border-radius)
      padding 1rem
      color var(--zeus-body-text)
      background-color var(--zeus-bg-tile)
      &:focus,
      &:hover
        color var(--zeus-primary)
        border-color var(--zeus-primary)
  .footer
    padding 2.5rem
    border-top 1px solid var(--zeus-body-border-medium)
    text-align center
    color var(--zeus-body-text-muted)
@media (max-width: $MQMobile)
  .homepage
    .hero
      img
        margin-right 1.6rem
      h1
        font-size 1.6rem
      .description
        font-size 1rem
    .features
      flex-direction column
    .feature,
    .topics div a
      flex 1 1 40%
@media (max-width: $MQMobileNarrow)
  .homepage
    .hero
      h1
        font-size 1.6rem
      img
        margin-right 0
      .description
        display none
      .action-button
        font-size 1rem
        padding 0.6rem 1.2rem
    .feature
      h2
        font-size 1.25rem
    .topics div a
      flex 1 1 100%
</style>
