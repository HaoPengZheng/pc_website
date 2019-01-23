<script>
export default {
  props: {
    type: {
      type: String,
      required: false,
      default: 'default'
    },
    span: {
      type: Number,
      required: false,
      default: 12
    }
  },
  data() {
    return {

    }
  },
  render(createElement) {
    let cardName
    switch (this.type) {
      case 'default':
        cardName = 'md-card'
        break
      case 'none':
        cardName = 'div'
        break
      case 'element':
        cardName = 'el-card'
        break
      default:
        cardName = 'md-card'
        break
    }
    return createElement(
      // el-col 百分比
      'el-col',
      {
        props: {
          span: this.span
        }
      },
      [
        createElement(
          cardName,
          {
            style: 'min-height:100px'
          },
          [this.$slots.default]
        )
      ],
    )
  }
}
</script>

<style lang="scss">
.md-card{
  background: #fff;
}
</style>

