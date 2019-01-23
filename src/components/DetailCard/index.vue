<template>
  <div :style="{width:width+'px'}" class="chunk-div">
    <slot :detailControl="detailControl" name="content"/>
  </div>
</template>
<script>

export default {
  props: {
    width: {
      type: String,
      required: false,
      default: ''
    },
    height: {
      type: String,
      required: false,
      default: ''
    }
  },
  data() {
    return {
      detailControl: {
        detailVisible: false,
        detailName: ''
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.chunk-div{
  position: relative;
}
</style>
