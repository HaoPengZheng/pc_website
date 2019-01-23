<template>
  <md-button
    :class="{'md-raised':active}"
    :style="styleObject"
  >
    <div>
      <slot/>
    </div>
  </md-button>
</template>

<script>
export default {
  props: {
    active: {
      type: Boolean,
      required: false,
      default: false
    },
    activeColor: {
      type: String,
      required: true
    }
  },
  data() {
    return {
    }
  },
  computed: {
    styleObject() {
      if (this.active) {
        return {
          background: this.activeColor,
          color: '#fff'
        }
      } else {
        return {
          background: '',
          color: ''
        }
      }
    }
  }
}
</script>
