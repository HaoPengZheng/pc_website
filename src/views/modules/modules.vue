<template>
  <div class="guider">
    <div>
      <el-row>
        <h2>
          豆腐块[bean-curd]
        </h2>
        <p>基本样式,2分版</p>
      </el-row>
      <el-row :gutter="20">
        <bean-curd />
        <bean-curd />
      </el-row>
      <el-row>
        <p>2/3,1/3版</p>
      </el-row>
      <el-row :gutter="20">
        <bean-curd :span="16" />
        <bean-curd :span="8" />
      </el-row>
      <el-row>
        <p>类型</p>
      </el-row>
      <el-row :gutter="20">
        <bean-curd
          :span="8"
          type="none"
        >
          <p>type:none</p>
          <p>类型:无样式</p>
        </bean-curd>
        <bean-curd :span="8" >
          <p>type:default</p>
          <p>类型:默认样式</p>
        </bean-curd>
        <bean-curd
          :span="8"
          type="element"
        >
          <p>type:element</p>
          <p>类型:饿了吗样式</p>
        </bean-curd>
      </el-row>
      <el-row>
        <h3>
          Attribute
        </h3>
      </el-row>
      <el-row>
        <el-table :data="attributeData" border>
          <el-table-column prop="param" label="参数"/>
          <el-table-column prop="explain" label="说明"/>
          <el-table-column prop="type" label="类型"/>
          <el-table-column prop="value" label="可选值"/>
          <el-table-column prop="default" label="默认值"/>
        </el-table>
      </el-row>
    </div>
  </div>
</template>

<script>
import BeanCurd from '@/components/BeanCurd/index'
export default {
  components: {
    BeanCurd
  },
  data() {
    return {
      attributeData: [
        {
          param: 'type',
          explain: '豆腐块类型选择',
          type: 'String',
          value: 'default/none/element',
          default: 'default'
        },
        {
          param: 'span',
          explain: '宽度选择，一共分24份，若要半版，则值为12',
          type: 'Number',
          value: '0-24',
          default: '12'
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

