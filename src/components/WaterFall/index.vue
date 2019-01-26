<template>
  <div>
    <!-- 垂直形式 -->
    <div
      v-loading="loading"
      v-if="vertical"
      :style="styleObject"
      class="md-layout waterfall"
      element-loading-text="拼命加载中"
      element-loading-spinner="el-icon-loading"
      element-loading-background="rgba(0, 0, 0, 0.8)"
    >
      <div
        v-for="(renderCol,index) in renderData"
        :key="index"
        :ref="`fall_${index}`"
        :class="classObject"
      >
        <md-card
          v-for="(item,index) in renderCol"
          :key="index"
        >

          <md-card-media>
            <img
              :src="item.attach"
              alt="People"
            >
          </md-card-media>

          <md-card-content>
            <code-render>{{ item.feed_content }}</code-render>
          </md-card-content>

          <md-card-actions>
            <div class="card-footer">
              <span class="user">{{ item.uname }}</span>
              <span class="time">{{ item.publish_time }}</span>
            </div>
          </md-card-actions>
        </md-card>
      </div>
      <div class="addmore">
        <md-button
          v-show="isComplete"
          disabled
        >没有更多</md-button>
        <md-button
          v-show="!isComplete"
          class="md-primary"
          @click.native="addMore"
        >加载更多
          <font-awesome-icon icon="angle-down" />
        </md-button>
      </div>
    </div>

    <!-- 水平形式 -->
    <div
      v-loading="loading"
      v-if="!vertical"
      :style="styleObject"
      class="waterfall horizontal"
      element-loading-text="拼命加载中"
      element-loading-spinner="el-icon-loading"
      element-loading-background="rgba(0, 0, 0, 0.8)"
    >
      <div
        v-for="(item,index) in alldata"
        :key="index"
        :ref="`fall_${index}`"
        :class="classObject"
      >
        <md-card>
          <md-card-media>
            <img
              :src="item.attach"
              alt="People"
            >
          </md-card-media>
          <md-card-content>
            <code-render>{{ item.feed_content }}</code-render>
          </md-card-content>
          <md-card-actions>
            <div class="card-footer">
              <span class="user">{{ item.uname }}</span>
              <span class="time">{{ item.publish_time }}</span>
            </div>
          </md-card-actions>
        </md-card>
      </div>


      <!-- 加载更多 -->
      <div class="addmore">
        <md-button
          v-show="isComplete"
          disabled
        >没有更多</md-button>
        <md-button
          v-show="!isComplete"
          class="md-primary"
          @click.native="addMore"
        >加载更多
          <font-awesome-icon icon="angle-down" />
        </md-button>
      </div>
    </div>
  </div>
</template>

<script>
import CodeRender from './CodeRender.vue'
export default {
  components: {
    CodeRender
  },
  props: {
    url: {
      type: String,
      required: false,
      default: ''
    },
    urlOption: {
      type: Object,
      required: false,
      default: function() {
        return {}
      }
    },
    count: {
      type: Number,
      required: false,
      default: 5
    },
    vertical: {
      type: Boolean,
      required: false,
      default: true
    },
    width: {
      type: String,
      required: false,
      default: '0'
    },
    height: {
      type: String,
      required: false,
      default: ''
    },
    data: {
      type: Array,
      required: false,
      default: function() {
        return []
      }
    },
    dataOption: {
      type: Object,
      required: false,
      default: function() {
        return {}
      }
    }
  },
  data() {
    return {
      alldata: [
        { 'feed_id': 911,
          'type': 'postimage',
          'feed_content': '【御泉通宝】\n随时自由兑换，无需任何手续费\n等值兑换，等同现金，全场通用\n通宝等值现金，剩余可等值退还\n通宝长期有效，可带走下次使用\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉',
          'publish_time': '2018-10-26 10:34',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d20d0f9d08cd23b.jpg',
          'label':
            null },
        { 'feed_id': 910, 'type': 'postimage', 'feed_content': '坊间传闻：现任镇长三姨太任翠儿掌柜的<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E9%A3%9E%E5%8F%91%E9%92%B1%E5%BA%84>#飞发钱庄#</a>，荣获小汤镇衙门独家御泉通宝兑换权，凡私下非法兑换者即送官府惩治！<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉', 'publish_time': '2018-10-26 10:33', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d126b0f835eb98c.jpg', 'label': null },
        { 'feed_id': 908, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】车上，贴心的御式服务<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c565ff0b38b95c1.jpg', 'label': null }, { 'feed_id': 907, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】梁小姐是第一位乘坐御温泉专线到达御温泉的游客，她8:30出门，9:15坐上穿梭巴士，35分钟后到达珠海口岸，爱温泉的她本欲去澳门却被御温泉欢迎牌吸引上了专线车，40分钟到达御温泉，大叹：一路非常顺畅，香港到御温泉居然可以一日游，实在太方便了。<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a>', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c298ce3a17d4a0c.jpg', 'label': null }, { 'feed_id': 906, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】今日御温泉的小哥哥小姐姐成了港珠澳大桥珠海公路口岸一道靓丽的风景线~<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:29', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27bf6eb72dc0b3d1e.jpg', 'label': null }, { 'feed_id': 904, 'type': 'postimage', 'feed_content': '“港珠澳大桥御温泉专线”的开通，给香港游客带来了极大的便利！一起来听听在御温泉工作多年的香港籍老员工、斗门市民、御温泉专线第一位乘客他们的喜悦心情吧~戳：  https://mp.weixin.qq.com/s/x_oSTK-JNmvx2XWYZIKzAw  <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a><a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:25', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27b2b2f179bedf4c9.jpg', 'label': null }, { 'feed_id': 903, 'type': 'postimage', 'feed_content': '两年一度的航展又要来啦，航展迷的你绝对不要错过哦，这里有一份御温泉航展线路指南，请查收：https://mp.weixin.qq.com/s/3o8clPg1hQ3Q6yo8ZB_hXg\nPS：御温泉家游站提供航展公众日2018年11月9日-11月11日纸质门票代售。\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:24', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27ac38b092e71b3f6.jpg', 'label': null }, { 'feed_id': 902, 'type': 'postimage', 'feed_content': '御温泉万圣节装备已上线，来开启一场奇幻之旅吧！万圣节福利快戳:https://mp.weixin.qq.com/s/SC2z6FAfd8sdFvbjfu4WHA限10月25-27号购买，手快有，手慢无。[笑而不语][笑而不语]<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:23', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27a8c0c9a9c94687a.jpg', 'label': null }, { 'feed_id': 911,
          'type': 'postimage',
          'feed_content': '【御泉通宝】\n随时自由兑换，无需任何手续费\n等值兑换，等同现金，全场通用\n通宝等值现金，剩余可等值退还\n通宝长期有效，可带走下次使用\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉',
          'publish_time': '2018-10-26 10:34',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d20d0f9d08cd23b.jpg',
          'label':
            null },
        { 'feed_id': 910, 'type': 'postimage', 'feed_content': '坊间传闻：现任镇长三姨太任翠儿掌柜的<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E9%A3%9E%E5%8F%91%E9%92%B1%E5%BA%84>#飞发钱庄#</a>，荣获小汤镇衙门独家御泉通宝兑换权，凡私下非法兑换者即送官府惩治！<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉', 'publish_time': '2018-10-26 10:33', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d126b0f835eb98c.jpg', 'label': null },
        { 'feed_id': 908, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】车上，贴心的御式服务<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c565ff0b38b95c1.jpg', 'label': null }, { 'feed_id': 907, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】梁小姐是第一位乘坐御温泉专线到达御温泉的游客，她8:30出门，9:15坐上穿梭巴士，35分钟后到达珠海口岸，爱温泉的她本欲去澳门却被御温泉欢迎牌吸引上了专线车，40分钟到达御温泉，大叹：一路非常顺畅，香港到御温泉居然可以一日游，实在太方便了。<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a>', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c298ce3a17d4a0c.jpg', 'label': null }, { 'feed_id': 906, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】今日御温泉的小哥哥小姐姐成了港珠澳大桥珠海公路口岸一道靓丽的风景线~<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:29', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27bf6eb72dc0b3d1e.jpg', 'label': null }, { 'feed_id': 904, 'type': 'postimage', 'feed_content': '“港珠澳大桥御温泉专线”的开通，给香港游客带来了极大的便利！一起来听听在御温泉工作多年的香港籍老员工、斗门市民、御温泉专线第一位乘客他们的喜悦心情吧~戳：  https://mp.weixin.qq.com/s/x_oSTK-JNmvx2XWYZIKzAw  <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a><a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:25', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27b2b2f179bedf4c9.jpg', 'label': null }, { 'feed_id': 903, 'type': 'postimage', 'feed_content': '两年一度的航展又要来啦，航展迷的你绝对不要错过哦，这里有一份御温泉航展线路指南，请查收：https://mp.weixin.qq.com/s/3o8clPg1hQ3Q6yo8ZB_hXg\nPS：御温泉家游站提供航展公众日2018年11月9日-11月11日纸质门票代售。\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:24', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27ac38b092e71b3f6.jpg', 'label': null }, { 'feed_id': 902, 'type': 'postimage', 'feed_content': '御温泉万圣节装备已上线，来开启一场奇幻之旅吧！万圣节福利快戳:https://mp.weixin.qq.com/s/SC2z6FAfd8sdFvbjfu4WHA限10月25-27号购买，手快有，手慢无。[笑而不语][笑而不语]<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:23', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27a8c0c9a9c94687a.jpg', 'label': null },
        { 'feed_id': 911,
          'type': 'postimage',
          'feed_content': '【御泉通宝】\n随时自由兑换，无需任何手续费\n等值兑换，等同现金，全场通用\n通宝等值现金，剩余可等值退还\n通宝长期有效，可带走下次使用\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉',
          'publish_time': '2018-10-26 10:34',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d20d0f9d08cd23b.jpg',
          'label':
            null },
        { 'feed_id': 910, 'type': 'postimage', 'feed_content': '坊间传闻：现任镇长三姨太任翠儿掌柜的<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E9%A3%9E%E5%8F%91%E9%92%B1%E5%BA%84>#飞发钱庄#</a>，荣获小汤镇衙门独家御泉通宝兑换权，凡私下非法兑换者即送官府惩治！<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉', 'publish_time': '2018-10-26 10:33', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d126b0f835eb98c.jpg', 'label': null },
        { 'feed_id': 908, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】车上，贴心的御式服务<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c565ff0b38b95c1.jpg', 'label': null }, { 'feed_id': 907, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】梁小姐是第一位乘坐御温泉专线到达御温泉的游客，她8:30出门，9:15坐上穿梭巴士，35分钟后到达珠海口岸，爱温泉的她本欲去澳门却被御温泉欢迎牌吸引上了专线车，40分钟到达御温泉，大叹：一路非常顺畅，香港到御温泉居然可以一日游，实在太方便了。<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a>', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c298ce3a17d4a0c.jpg', 'label': null }, { 'feed_id': 906, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】今日御温泉的小哥哥小姐姐成了港珠澳大桥珠海公路口岸一道靓丽的风景线~<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:29', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27bf6eb72dc0b3d1e.jpg', 'label': null }, { 'feed_id': 904, 'type': 'postimage', 'feed_content': '“港珠澳大桥御温泉专线”的开通，给香港游客带来了极大的便利！一起来听听在御温泉工作多年的香港籍老员工、斗门市民、御温泉专线第一位乘客他们的喜悦心情吧~戳：  https://mp.weixin.qq.com/s/x_oSTK-JNmvx2XWYZIKzAw  <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a><a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:25', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27b2b2f179bedf4c9.jpg', 'label': null }, { 'feed_id': 903, 'type': 'postimage', 'feed_content': '两年一度的航展又要来啦，航展迷的你绝对不要错过哦，这里有一份御温泉航展线路指南，请查收：https://mp.weixin.qq.com/s/3o8clPg1hQ3Q6yo8ZB_hXg\nPS：御温泉家游站提供航展公众日2018年11月9日-11月11日纸质门票代售。\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:24', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27ac38b092e71b3f6.jpg', 'label': null }, { 'feed_id': 902, 'type': 'postimage', 'feed_content': '御温泉万圣节装备已上线，来开启一场奇幻之旅吧！万圣节福利快戳:https://mp.weixin.qq.com/s/SC2z6FAfd8sdFvbjfu4WHA限10月25-27号购买，手快有，手慢无。[笑而不语][笑而不语]<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:23', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27a8c0c9a9c94687a.jpg', 'label': null },
        { 'feed_id': 911,
          'type': 'postimage',
          'feed_content': '【御泉通宝】\n随时自由兑换，无需任何手续费\n等值兑换，等同现金，全场通用\n通宝等值现金，剩余可等值退还\n通宝长期有效，可带走下次使用\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉',
          'publish_time': '2018-10-26 10:34',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d20d0f9d08cd23b.jpg',
          'label':
            null },
        { 'feed_id': 910, 'type': 'postimage', 'feed_content': '坊间传闻：现任镇长三姨太任翠儿掌柜的<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E9%A3%9E%E5%8F%91%E9%92%B1%E5%BA%84>#飞发钱庄#</a>，荣获小汤镇衙门独家御泉通宝兑换权，凡私下非法兑换者即送官府惩治！<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​',
          'uname': '御温泉', 'publish_time': '2018-10-26 10:33', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27d126b0f835eb98c.jpg', 'label': null },
        { 'feed_id': 908, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】车上，贴心的御式服务<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30',
          'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c565ff0b38b95c1.jpg', 'label': null }, { 'feed_id': 907, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】梁小姐是第一位乘坐御温泉专线到达御温泉的游客，她8:30出门，9:15坐上穿梭巴士，35分钟后到达珠海口岸，爱温泉的她本欲去澳门却被御温泉欢迎牌吸引上了专线车，40分钟到达御温泉，大叹：一路非常顺畅，香港到御温泉居然可以一日游，实在太方便了。<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a>', 'uname': '御温泉', 'publish_time': '2018-10-26 10:30', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27c298ce3a17d4a0c.jpg', 'label': null }, { 'feed_id': 906, 'type': 'postimage', 'feed_content': '【港珠澳大桥御温泉专线首发礼精彩回放】今日御温泉的小哥哥小姐姐成了港珠澳大桥珠海公路口岸一道靓丽的风景线~<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a> <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:29', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27bf6eb72dc0b3d1e.jpg', 'label': null }, { 'feed_id': 904, 'type': 'postimage', 'feed_content': '“港珠澳大桥御温泉专线”的开通，给香港游客带来了极大的便利！一起来听听在御温泉工作多年的香港籍老员工、斗门市民、御温泉专线第一位乘客他们的喜悦心情吧~戳：  https://mp.weixin.qq.com/s/x_oSTK-JNmvx2XWYZIKzAw  <a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E6%B8%AF%E7%8F%A0%E6%BE%B3%E5%A4%A7%E6%A1%A5%E5%BE%A1%E6%B8%A9%E6%B3%89%E4%B8%93%E7%BA%BF>#港珠澳大桥御温泉专线#</a><a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:25', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27b2b2f179bedf4c9.jpg', 'label': null }, { 'feed_id': 903, 'type': 'postimage', 'feed_content': '两年一度的航展又要来啦，航展迷的你绝对不要错过哦，这里有一份御温泉航展线路指南，请查收：https://mp.weixin.qq.com/s/3o8clPg1hQ3Q6yo8ZB_hXg\nPS：御温泉家游站提供航展公众日2018年11月9日-11月11日纸质门票代售。\n<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:24', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27ac38b092e71b3f6.jpg', 'label': null }, { 'feed_id': 902, 'type': 'postimage', 'feed_content': '御温泉万圣节装备已上线，来开启一场奇幻之旅吧！万圣节福利快戳:https://mp.weixin.qq.com/s/SC2z6FAfd8sdFvbjfu4WHA限10月25-27号购买，手快有，手慢无。[笑而不语][笑而不语]<a href=http://i-wq.net/wqproject_company/index.php/66?app=public&mod=Feed&act=topic&k=%E7%8F%A0%E6%B5%B7%E5%BE%A1%E6%B8%A9%E6%B3%89>#珠海御温泉#</a> ​​​​', 'uname': '御温泉', 'publish_time': '2018-10-26 10:23', 'attach': 'http://i-wq.net/wqproject_company/data/upload/2018/1026/10/5bd27a8c0c9a9c94687a.jpg', 'label': null }
      ],
      flag: 0,
      col: 5,
      loading: false,
      isUrlData: true
    }
  },
  computed: {
    styleObject() {
      const styleObject = {}
      if (this.width !== '') {
        styleObject.minWidth = `${this.width}px`
      }
      if (this.height !== '') {
        styleObject.maxHeight = `${this.height}px`
      }
      return styleObject
    },
    classObject() {
      const classObject = {
        'md-layout-item': true
      }
      const className = 'md-size-' + 100 / this.count
      classObject[className] = true
      return classObject
    },
    renderData() {
      const renderData = new Array(this.count)
      let i = 0
      this.showData.forEach((item, index) => {
        if (!(renderData[i] instanceof Array)) {
          renderData[i] = []
        }
        renderData[i++].push(item)
        if (i % this.count === 0) {
          i = 0
        }
      })
      return renderData
    },
    showData() {
      let showData = []
      showData = this.alldata.slice(0, this.flag)
      return showData
    },
    isComplete() {
      return this.flag === this.alldata.length
    }
  },
  created() {
    this.init()
  },
  methods: {
    init() {
      /*
        初始化轮播图
        判断是否为url模式=>{

          urlOption:{
            method: 'GET',
            param: '参数',
            map:{
              attach:''//图片
              feed_content:''内容
              uname: '' //发布人名
              publish_time:'' 时间
            }
          }
          url模式=> 拉取数据

          数据模式=> 导入所有数据
        }
      */
      if (this.url !== '') {
        this.isUrlData = true
        this.initUrlMode()
      }
      if (this.data.length !== 0 && this.url === '') {
        this.isUrlData = false
      }
      this.isUrlData = false
      if (this.isUrlData) {
        this.flag = 0
      } else {
        this.addFlag()
      }
    },
    initUrlMode() {
      console.log('url-mode')
      this.$axios({
        methods: 'get',
        url: this.url
      }).then(response => {
        console.log(response)
      })
    },
    addFlag() {
      this.flag = this.flag + this.dataOption.item > this.alldata.length ? this.alldata.length : this.flag + this.dataOption.item
    },
    addMore() {
      this.loading = true
      if (!this.isUrlData) {
        this.addFlag()
      }
      setTimeout(() => {
        this.loading = false
      }, 1000)
    }
  }
}
</script>

<style lang="scss" scoped>
.md-card {
  margin: 10px 10px;
  min-width: 200px;
}
.waterfall {
  overflow: auto;
  padding: 0 20px;
}
.addmore {
  display: flex;
  justify-content: center;
  width: 100%;
}
.card-footer {
  display: flex;
  justify-content: space-between;
  width: 100%;
  align-items: center;
  .user {
    color: #00a7e1;
    text-decoration: none;
  }
  .time {
    height: 30px;
    line-height: 30px;
    padding: 5px 0;
    color: #aaa;
  }
}
.horizontal {
  display: flex;
  flex-wrap: nowrap;
  overflow: auto;
  .md-card {
    height: 500px;
    img {
      height: 300px;
    }
    .md-card-content {
      overflow: hidden;
      text-overflow: ellipsis; //文本溢出显示省略号
      display: -webkit-box;
      -webkit-line-clamp: 5;
      -webkit-box-orient: vertical;

    }
  }
}
</style>

