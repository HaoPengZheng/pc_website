<template>
  <div v-show="isActive">
    <slot/>
  </div>
</template>
<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    name: {
      type: String,
      require: true,
      default: ''
    }
  },
  data() {
    return {
      isAcive: false
    }
  },
  computed: {
    getActiveIndex() {
      return this.$parent.index
    },
    isActive() {
      return this.getActiveIndex === this.name
    }
  }
}
</script>
