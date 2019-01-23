
<script>
export default {
  created() {
  },
  mounted() {
    this.$refs.content.innerHTML = this.$slots.default[0].text
  },
  render(createElement) {
    return createElement(
      'div',
      {
        class: 'content',
        ref: 'content'
      },
      [this.$slots.default]
    )
  }
}
</script>

<style lang="scss" scoped>
.content{
  table-layout: fixed;
  word-break: break-all;
  overflow: hidden;
}
</style>

