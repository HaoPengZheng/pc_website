<template>
  <div class="guider">
    <div>
      <el-row>
        <h2>
          Tab标签页[diy-tab]
        </h2>
        <p>基本样式</p>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="12">
          <diy-tab
            title="主题游"
            type="tab"
            color="#21c09e"
            active
          >
            <diy-tab-item
              name="first"
              label="动态"
            >Tab形式1</diy-tab-item>
            <diy-tab-item
              name="second"
              label="商品"
            >Tab形式2</diy-tab-item>
          </diy-tab>
        </el-col>
        <el-col :span="12">
          <diy-tab
            color="red"
            title="小汤镇"
          >
            非Tab形式
          </diy-tab>
        </el-col>
      </el-row>
      <el-row>
        <h3>
          [diy-tab] Attribute
        </h3>
      </el-row>
      <el-row>
        <el-table
          :data="attributeData"
          border
        >
          <el-table-column
            prop="param"
            label="参数"
          />
          <el-table-column
            prop="explain"
            label="说明"
          />
          <el-table-column
            prop="type"
            label="类型"
          />
          <el-table-column
            prop="value"
            label="可选值"
          />
          <el-table-column
            prop="default"
            label="默认值"
          />
        </el-table>
      </el-row>
      <el-row>
        <h3>
          [diy-tab-item] Attribute
        </h3>
      </el-row>
      <el-row>
        <el-table
          :data="tabItemAttributeData"
          border
        >
          <el-table-column
            prop="param"
            label="参数"
          />
          <el-table-column
            prop="explain"
            label="说明"
          />
          <el-table-column
            prop="type"
            label="类型"
          />
          <el-table-column
            prop="value"
            label="可选值"
          />
          <el-table-column
            prop="default"
            label="默认值"
          />
        </el-table>
      </el-row>
    </div>
  </div>
</template>

<script>
import DiyTab from '@/components/DiyTab/index'
import DiyTabItem from '@/components/DiyTab/DiyTabItem'
export default {
  components: {
    DiyTab,
    DiyTabItem
  },
  data() {
    return {
      attributeData: [
        {
          param: 'title',
          explain: '标题',
          type: 'String',
          value: '-',
          default: '-'
        },
        {
          param: 'color',
          explain: '颜色，传入颜色代码',
          type: 'String',
          value: '-',
          default: '#000'
        },
        {
          param: 'type',
          explain: '类型',
          type: 'String',
          value: 'tab/none',
          default: 'tab'
        }
      ],
      tabItemAttributeData: [
        {
          param: 'name',
          explain: 'TAB名，用于检索tab内容',
          type: 'String',
          value: '-',
          default: '-'
        },
        {
          param: 'label',
          explain: '标签',
          type: 'tab按钮显示的名称',
          value: '-',
          default: '-'
        }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.guider {
  padding: 1vh 2vw;
  background: #f7f7f7;
  min-height: 80vh;
}
.md-card {
  min-height: 100px;
  background: #fff;
}
</style>

