<template>
  <div>
    <div
      title="查看详情"
      @click="show"
    >
      <slot name="context"/>
    </div>
    <div
      v-show="detailVisible"
      class="detail "
    >
      <div class="detail-context ">
        <slot name="detail"/>
      </div>
      <div class="detail-footer">
        <md-button
          class="md-dense md-raised md-primary"
          @click="close"
        >关闭</md-button>
      </div>
      <span class="lt"/>
      <!-- <span class="rb"/> -->
    </div>

  </div>
</template>
<script>
export default {
  data() {
    return {
      detailVisible: false
    }
  },
  methods: {
    show() {
      this.detailVisible = true
    },
    close() {
      this.detailVisible = false
    }
  }
}
</script>
<style lang="scss" scoped>
.detail {
  color: aliceblue;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  width: 100%;
  z-index: 2;
  border:0.5rem solid #ae7548;
}
.detail-context {
  height: 100px;
  position: absolute;
  bottom: 45px;
  top: 0;
  overflow: auto;
  width:100%;
  height: 100%;
}
.detail-footer {
  z-index: 3;
  position: absolute;
  bottom: 0;
  right: 0;
}
.lt {
    position: absolute;
    left: 0;
    top: 0;
    width: 11rem;
    height: 5rem;
    background: url('../../assets/images/cloud.png') no-repeat left top;
    background-size: contain;
    transform: rotateY(180deg) translate(30%, -50%);
}
.rb {
    position: absolute;
    right: 0;
    top: -5rem;
    width: 11rem;
    height: 5rem;
    background: url('../../assets/images/cloud.png') no-repeat left top;
    background-size: 100% 100%;
    transform: translate(30%, 50%);
}
</style>

