<template>
  <div
    :style="styleObject"
    class="diy-box"
  >
    <div class="diy-box-header">
      <div
        :style="styleObject"
        class="header-text"
      >
        <span >
          {{ title }}
        </span>
        <font-awesome-icon
          :style="styleObject"
          icon="qrcode"
        />
      </div>
      <slot name="header-right"/>
      <div class="header-nav">
        <my-button v-for="tab in tabsPropsData" :key="tab.name" :active="tab.name == index" :active-color="color" @click.native="changeTab(tab.name)">
          {{ tab.label }}
        </my-button>
      </div>
    </div>
    <div class="diy-box-content" >
      <slot :active="index"/>
    </div>
  </div>
</template>
<script>
import MyButton from './MyButton.vue'
export default {
  components: {
    MyButton
  },
  props: {
    title: {
      type: String,
      required: true
    },
    color: {
      type: String,
      required: false,
      default: '#000'
    },
    type: {
      type: String,
      required: false,
      default: 'tab'
    }
  },
  data() {
    return {
      styleObject: {
        color: 'red'
      },
      tabsPropsData: [],
      index: 'first'
    }
  },
  created() {
    this.styleObject.color = this.color
    this.initBoxItem()
  },
  methods: {
    initBoxItem() {
      if (typeof this.$slots.default === 'undefined') {
        return
      } else if (this.type === 'tab') {
        this.$slots.default.forEach(vnode => {
          if (vnode.tag !== undefined && vnode.tag.indexOf('diy-tab-item') !== -1) {
            this.tabsPropsData.push(vnode.componentOptions.propsData)
          }
        })
      }
      if (this.tabsPropsData.length > 0) {
        this.index = this.tabsPropsData[0].name
      }
    },
    changeTab(activeName) {
      this.index = activeName
    }
  }
}
</script>

<style lang="scss" scoped>
.diy-box {
  margin: 20px 10px;
  .diy-box-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
    .header-text {
      display: flex;
      justify-content: flex-start;
      font-family: "by4-jojisin";
      font-size: 26px;
      font-weight: 500;
      display: inline-block;
      padding: 0 10px 0 5px;
      line-height: 40px;
      color: #000;
      height: 40px;
      &::before {
        content: "";
        display: inline-block;
        border: 7px solid;
        border-right-color: transparent;
        border-bottom-color: transparent;
        vertical-align: top;
      }
      span {
        color: #000;
      }
    }
    .header-nav {
    }
  }
  .diy-box-content {
    padding: 5px 10px;
    background: #fff;
    color:#000;
    box-shadow: 0 3px 1px -2px rgba(0,0,0,.2), 0 2px 2px 0 rgba(0,0,0,.14), 0 1px 5px 0 rgba(0,0,0,.12);
    position: relative;
    z-index: 1;
    border-radius: 2px;
    transition: .3s cubic-bezier(.4,0,.2,1);
    transition-property: color,background-color;
    will-change: color,background-color;
    box-shadow: 0 3px 1px -2px rgba(0,0,0,.2), 0 2px 2px 0 rgba(0,0,0,.14), 0 1px 5px 0 rgba(0,0,0,.12);
  }
}
</style>
