<template lang='pug'>
  button.button-back(v-if='canGoBack', @click='goBack')
    svg.icon
      use(xlink:href='/icons.svg#arrow-left-alt')
</template>

<script>
export default {
  methods: {
    canGoBack () {
      window.history.length > 1
    },
    goBack () {
      this.$router.go(-1)
    }
  }
}
</script>

<style scoped lang="stylus">
.button-back
  position absolute
  z-index 2
  top 16px
  left 0
  border 0
  background transparent
  border-radius 50%
  cursor pointer
.icon
  width 32px
  height 32px
.mobile
  .button-back
    top 14px
  .icon
    width 26px
    height 26px
</style>
