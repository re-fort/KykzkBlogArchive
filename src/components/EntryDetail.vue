<template lang="pug">
  .columns
    .column.is-8.is-offset-2
      a.button.is-light.is-loading(v-show="isLoading")
      article(v-for="entry in selectedEntries")
        div.innerHead
          div.box-date
            time
              | {{ entry.date | YYYY.MM }}
            time
              | {{ entry.date | DD }}
          div.box-ttl
            h3
              | {{ entry.title }}
            p.name
              | {{ author.name }}
          div.box-sns
        div.box-article(v-html="entry.body")
        div.footer-wrapper
          div.twitter-share-button-wrapper
            a.twitter-share-button(href="https://twitter.com/share?ref_src=twsrc%5Etfw", :data-text="entry.title", :data-url="'https://re-fort.net/KykzkBlogArchive/#/blog/'+author.link+'/'+date+'/'+entry.id", data-size="large" data-show-count="false")
              | ツイート
          div
            router-link(:to="date+'/'+entry.id")
              | 個別ページ
        Adsense(data-ad-client="ca-pub-6267609390272538" data-ad-slot="8585572114")
</template>

<script>
  import Adsense from 'vue-google-adsense/dist/Adsense.min.js'
  Vue.use(require('vue-script2'))
  Vue.use(Adsense)

  export default {
    name: 'EntryDetail',
    props: {
      author: {
        type: Object,
      },
      entries: {
        type: Array,
      },
      id: {
        type: String,
      },
      date: {
        type: String,
      },
      isLoading: {
        type: Boolean,
      },
    },
    updated () {
      if (window.twttr) {
        window.twttr.widgets.load();
      }
    },
    computed: {
      selectedEntries () {
        const entry = this.entries.filter(entry => this.id === entry.id);
        return entry
      },
    },
  }
</script>

<style lang="sass" scoped>
  @import "src/stylesheets/variables"

  .is-loading
    width: 100%

  article
    padding: 24px 0 0 0
    border-top: 1px solid $main-color
    border-bottom: 1px solid $main-color

    .innerHead
      &:after
        content: ""
        display: block
        clear: both

      .box-date
        float: left
        margin-right: 20px
        background-color: $main-color
        width: 74px
        height: 74px
        text-align: center

        time
          color: #fff
          text-align: center
          display: inline-block

          &:first-child
            font-size: 12px
            margin-top: 5px

          &:nth-child(2)
            font-size: 38px

      .box-ttl
        float: left

        h3
          font-size: 28px
          color: #8d8d8d
          margin: 0

        p.name
          font-size: 18px
          color: #77c059
          margin: 0

      .box-sns
        clear: both
        float: left
        margin: 10px 0 30px 0

    .box-article
      word-break: break-all
      font-size: 15px
      border-top: 1px solid #d2d2d2
      border-bottom: 1px solid #d2d2d2
      padding-top: 40px
      padding-bottom: 30px
      margin-bottom: 2rem

    .adswrapper
      margin-bottom: 20px
      max-height: 300px

  .footer-wrapper
    display: flex
    justify-content: flex-start
    margin-bottom: 2rem

  .twitter-share-button-wrapper
    margin-right: auto

  @media screen and (max-width: 640px)
    article
      .innerHead
        .box-ttl
          width: 220px
</style>
