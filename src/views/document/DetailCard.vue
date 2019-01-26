<template>
  <div class="guider">
    <div>
      <el-row>
        <h2>
          细节卡片[detail-card]
        </h2>
        <p>基本样式</p>
      </el-row>
      <el-row :gutter="20">
        <el-col :span="12" :offset="6">
          <detail-card>
            <template slot="content">
              <div class="md-layout">
                <div class="md-layout-item md-size-50 md-medium-size-66 md-small-size-100 md-xsmall-size-100">
                  <detail-item>
                    <div slot="context">
                      <md-card md-with-hover>
                        <md-card-content>
                          <img src="http://192.168.101.110/pc/pc/index/img/goods_2.jpg" style="width:100%;height:100%">
                        </md-card-content>
                      </md-card>
                    </div>
                    <template slot="detail">
                      <iframe
                        src="http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Personal&act=shopIndex"
                      />
                    </template>
                  </detail-item>
                </div>
                <div class="md-layout-item md-size-50 md-medium-size-66 md-small-size-100 md-xsmall-size-100">
                  <detail-item>
                    <div slot="context">
                      <md-card md-with-hover>
                        <md-card-content>
                          <img src="https://www.baidu.com/img/bd_logo1.png" style="width:100%;height:100%">
                        </md-card-content>
                      </md-card>
                    </div>
                    <template slot="detail">
                      <iframe
                        src="https://wwww.baidu.com"
                      />
                    </template>
                  </detail-item>
                </div>
                <div class="md-layout-item md-size-50 md-medium-size-66 md-small-size-100 md-xsmall-size-100">
                  <detail-item>
                    <div slot="context">
                      <md-card md-with-hover>
                        <md-card-content>
                          <img src="http://192.168.101.110/pc/pc/index/img/goods_2.jpg" style="width:100%;height:100%">
                        </md-card-content>
                      </md-card>
                    </div>
                    <template slot="detail">
                      <iframe
                        src="http://www.00800.com.cn/cnhs/wqproject/index.php?app=public&mod=PCNew&act=index"
                      />
                    </template>
                  </detail-item>
                </div>
                <div class="md-layout-item md-size-50 md-medium-size-66 md-small-size-100 md-xsmall-size-100">
                  <detail-item>
                    <div slot="context">
                      <md-card md-with-hover>
                        <md-card-content>
                          <img src="http://192.168.101.110/pc/pc/index/img/goods_2.jpg" style="width:100%;height:100%">
                        </md-card-content>
                      </md-card>
                    </div>
                    <template slot="detail">
                      <iframe
                        src="http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Personal&act=shopIndex"
                      />
                    </template>
                  </detail-item>

                </div>

            </div></template>
          </detail-card>
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
import DetailCard from '@/components/DetailCard/index'
import DetailItem from '@/components/DetailCard/DetailItem'
export default {
  components: {
    DetailCard,
    DetailItem
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
  height: 250px;
  background: #fff;
}
.md-card-content{
  height: 100%;
  width: 100%;
}
iframe{
  border: 0;
  width: 100%;
  height:100%;
}
</style>

