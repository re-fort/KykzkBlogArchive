<template lang="pug">
  .columns
    .column.is-8.is-offset-2
      a.button.is-light.is-loading(v-show="isLoading")
      article(v-for="entry in sortedEntries")
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
</template>

<script>
  export default {
    name: 'Entry',
    props: {
      author: {
        type: Object,
      },
      entries: {
        type: Array,
      },
      sort: {
        type: String,
        default: 'date',
      },
      order: {
        type: String,
        default: 'asc',
      },
      sortEntries: {
        type: Function,
      },
      isLoading: {
        type: Boolean,
      },
    },
    computed: {
      sortedEntries () {
        return this.sortEntries(this.sort, this.order)
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

  @media screen and (max-width: 640px)
    article
      .innerHead
        .box-ttl
          width: 220px
</style>
