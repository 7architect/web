<template lang="pug">
main
  .stack
    .stack__item
      h1.title.title--size-xlarge.title--weight-normal.title--align-center Alexander Katkov
      .title.title--level-2 developer, musician
    .stack__item
      .container
        p Hello! I am a front-end developer based in Saint Petersburg, with experience in Vue and React. I specialize in building scalable microservice projects from the ground up and designing robust architectures.
        p I have a strong interest in blockchain, cryptography, and P2P technologies. In my free time, I create electronic music (industrial, trance), experiment with Ableton Live and FabFilter, and develop services for sharing audio samples and presets.
        p I value organization, continuous learning, and exploring technologies that expand human perception. I am always open to new projects, ideas, and challenging tasks.


    .stack__item: .container: nuxt-link(to="/contact"): v-button contact me via ...

  timeline(:timeline="$store.state.timeline")
</template>

<script>
  import { mapActions, mapGetters } from 'vuex'
  import Scroll from 'vuescroll'
  import VButton from '~/components/button/button'
  import Timeline from '~/components/timeline/timeline'
  import TimelineEvent from '~/components/timeline/timeline-event'

  export default {
    components: {
      Scroll,
      VButton,
      Timeline,
      TimelineEvent
    },

    data() {
      return { interval: null }
    },

    computed: {
      ...mapGetters([
        'timeline'
      ])
    },
    methods: {
      ...mapActions([
        'loadTimeline'
      ]),
      load() {
        this.loadTimeline()
      }
    },
    mounted() {
      this.interval = setInterval(this.load, 5000)
    },
    beforeDestroy() {
      clearInterval(this.interval)
    },
    async middleware({ store }) {
      await store.dispatch('loadTimeline')
    }
  }
</script>

<style lang="stylus">
  @import '../assets/stylus/variables/colors.styl'

  .present
    width 500px
    margin 0 auto
    &__alpha-annotation
      font-size .8em
      margin-top .5em
      text-align center
      color #f99
      opacity .5
  .stack
    &__item
      text-align center
      &:not(:last-of-type)
        &::after
          background: linear-gradient(0deg, transparent, $color.grey, transparent)
          display block
          content ""
          width 1px
          height 50px
          margin 1rem auto
      &-title
        color: $color.white
        font-weight 400
        font-size 1.5em
        letter-spacing 3px
      &-desc
        color: darken($color.grey, 20)
        font-weight 200
        letter-spacing 1px;
</style>
