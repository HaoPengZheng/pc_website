<template>
  <div class="guider">
    <div>
      <el-row>
        <h2>
          瀑布流[water-fall]
        </h2>
        <p>基本样式</p>
      </el-row>
      <el-row :gutter="20">
        <water-fall :count="5" :data-option="{item:3}" width="1080"/>
      </el-row>
      <el-row>
        <p>水平滚动</p>
      </el-row>
      <el-row :gutter="20">
        <water-fall :vertical="false" :count="5" :data-option="{item:8}" width="1080"/>
      </el-row>
      <el-row>
        <p>通过url映射数据</p>
      </el-row>
      <el-row :gutter="20">
        <water-fall
          :count="5"
          :data-option="{item:8}"
          :url-option="urlOption"
          url="http://www.00800.com.cn/cnhs/wqproject/index.php?app=public&mod=PCNew&act=getCompanyIndexFeeds&start=0"
          width="1080"/>
      </el-row>
      <el-row>
        <h3>
          [water-fall] Attribute
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
    </div>
  </div>
</template>

<script>
import WaterFall from '@/components/WaterFall/index'
export default {
  components: {
    WaterFall
  },
  data() {
    return {
      urlOption: {
        method: 'Get'

      },
      attributeData: [
        {
          param: 'url',
          explain: '请求数据资源的url',
          type: 'String',
          value: '-',
          default: '-'
        },
        {
          param: 'urlOption',
          explain: 'url配置项,为了匹配不同请求返回的数据格式,参数有img,text,user,time',
          type: 'Object',
          value: '-',
          default: '-'
        },
        {
          param: 'count',
          explain: '列数/行数',
          type: 'Number',
          value: '-',
          default: '5'
        },
        {
          param: 'vertical',
          explain: '是否为垂直方向',
          type: 'Boolean',
          value: 'true/false',
          default: 'true'
        },
        {
          param: 'width',
          explain: '设置最小宽度，不在缩小',
          type: 'String',
          value: '-',
          default: '-'
        },
        {
          param: 'height',
          explain: '高度限制',
          type: 'String',
          value: '-',
          default: '-'
        },
        {
          param: 'moreParam',
          explain: '加载更多的参数',
          type: 'String',
          value: '-',
          default: '-'
        },
        {
          param: 'data',
          explain: '传入已组织好的数据格式,所有数据',
          type: 'Object',
          value: '-',
          default: '-'
        },
        {
          param: 'dataOption',
          explain: '配置组织数据,item:条数',
          type: 'Object',
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

