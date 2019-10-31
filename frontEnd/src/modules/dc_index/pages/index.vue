<template>
  <div class="home-index">
    <!-- 图表 -->
    <div id="echarts" style="width:1200px;height:600px;"></div>
    <!-- 卡片轮播 -->
    <!-- <carousel></carousel>
    <div class="forum-good">
      <div class="good-header">
        <h3>论坛精选</h3>
        <div class="tip-line">
          <span></span>
        </div>
      </div>
      <ul class="good-list">
        <li v-for="(item, index) in goodList" :key="index">
          <a href="#">
            <div class="img-box">
              <img :src="rootPath+item.imgPath">
            </div>
          </a>
          <div class="good-detail">
            <a href="#">
              <img :src="item.headImg">
            </a>
            <a href="#">{{item.smallName}}</a>
            <span class="see">{{item.seeNum}}</span>
            <span class="message">{{item.messageNum}}</span>
          </div>
        </li>
      </ul>
    </div>-->
    <!-- 时装资讯 -->
    <!-- <md-list v-for="(item,index) of conList" :key="index" :item="item"></md-list>
    <div class="post">
      <el-button type="primary" icon="el-icon-edit el-icon--top" @click="goPostForum">发帖</el-button>
    </div>-->
  </div>
</template>
<script>
import mdList from "../components/mdList.vue";
import carousel from "../components/carousel.vue";

export default {
  name: "index_content",
  data() {
    return {
      currentDate: "精彩",
      conList: [],
      rootPath,
      goodList: [
        {
          smallName: "我的一棵小小草",
          headImg: require("../../../assets/images/bg1.jpg"),
          imgPath: "/index/dress_coll2.png",
          seeNum: "120",
          messageNum: "14"
        },
        {
          smallName: "我的一棵小小草",
          headImg: require("../../../assets/images/bg1.jpg"),
          imgPath: "/index/dress_coll2.png",
          seeNum: "120",
          messageNum: "14"
        },
        {
          smallName: "我的一棵小小草",
          headImg: require("../../../assets/images/bg1.jpg"),
          imgPath: "/index/dress_coll2.png",
          seeNum: "120",
          messageNum: "14"
        },
        {
          smallName: "我的一棵小小草",
          headImg: require("../../../assets/images/bg1.jpg"),
          imgPath: "/index/dress_coll2.png",
          seeNum: "120",
          messageNum: "14"
        }
      ]
    };
  },
  components: {
    mdList,
    carousel
  },
  created() {
    // let url = "/api/mdList.json";
    // client.request(url).then(
    //   res => {
    //     this.conList = res.body;
    //   },
    //   err => {
    //     console.log(err);
    //   }
    // );
  },
  mounted() {
    let echarts = require("../../../assets/js/echarts.min.js").echarts;
    let myECharts = echarts.init(document.getElementById("echarts"));
    let now = new Date();
    let date = [];
    let barData = [];
    for (let i = 0; i < 30; i++) {
      let tempdate = new Date(now.getTime() + 24 * 60 * 60 * 1000 * i);
      date.push(
        [
          tempdate.getFullYear(),
          tempdate.getMonth() + 1,
          tempdate.getDate()
        ].join("/")
      );
      barData.push(Math.round(Math.random() * 200));
    }
    let option = {
      backgroundColor: "#110f42",
      title: {
        text: "监控管理",
        left: "center",
        textStyle: {
          color: "#fff"
        }
      },
      tooltip: {
        trigger: "axis",
        axisPointer: {
          //鼠标指向位置
          type: "shadow"
        }
      },
      xAxis: {
        axisTick: {
          show: false
        },
        axisLabel:{
          rotate: 45 //旋转
        },
        axisLine: {
          lineStyle: {
            color: "#fff"
          }
        },
        data: date
      },
      yAxis: {
        name: '单位1',
        nameTextStyle:{
          color: '#43eec6',
          padding: [10,0,10,0]
        },
        nameGap: 15,
        type: "value",
        axisTick: false,
        axisLine: {
          show: false,
          lineStyle: {
            color: "#fff"
          }
        },
        splitLine: {
          //分割线-grid区域
          show: true,
          lineStyle: {
            type: "dashed",
            color: "#ccc"
          }
        }
      },
      dataZoom: [
        {
          type: 'inside',
          start: 0,
          end: 10,
          xAxisIndex: [0],
          filterMode: "filter"
        },
        {
          type: 'slider',
          start: 0,
          end: 10,
          show: true,
          xAxisIndex: [0],
          handleIcon: 'image://https://www.echartsjs.com/zh/images/logo.png',
          dataBackground:{
            type: 'solid',
            lineStyle:{
              color: '#43eec6',
              width: 2
            }
          },
          borderColor: '#110f42'
        }
      ],
      series: [
        {
          name: "柱状图",
          type: "bar",
          barWidth: 10,
          barCategoryGap: 40,
          // barGap: '100%',
          // boundaryGap: 10,
          itemStyle: {
            barBorderRadius: [5, 5, 0, 0],
            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
              { offset: 0, color: "#14c8d4" },
              { offset: 1, color: "#43eec6" }
            ]),
            emphasis: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: "#efd1a4" },
                { offset: 1, color: "#ef9802" }
              ])
            }
          },
          data: barData,
        }
      ]
    };
    myECharts.setOption(option);
  },
  methods: {
    goPostForum() {
      this.$router.push({ name: "post_forum" });
    }
  }
};
</script>

<style lang="less">
.home-index {
  .forum-good {
    width: 90%;
    margin: 0 auto;
    max-width: 1800px;
    min-width: 1000px;
    .good-header {
      h3 {
        width: 100%;
        height: 50px;
        margin: 30px 0 10px 0;
        text-align: center;
        font: normal 28px/50px "Microsoft YaHei", Arial;
        color: #333;
      }
      .tip-line {
        display: flex;
        justify-content: center;
        span {
          width: 30px;
          height: 2px;
          background-color: #409eff;
          text-align: center;
        }
      }
    }
    .good-list {
      margin-top: 20px;
      display: flex;
      justify-content: center;
      li {
        margin-right: 20px;
        box-shadow: 2px 3px 8px rgba(0, 0, 0, 0.2);
        .img-box {
          width: 300px;
          height: 200px;
          padding: 10px 0;
          border-bottom: 1px solid #e0e0e0;
          img {
            width: 100%;
            height: 100%;
          }
        }
        .good-detail {
          height: 50px;
          display: flex;
          align-items: center;
          & > a {
            padding-left: 5px;
          }
          img {
            width: 30px;
            height: 30px;
            border-radius: 50%;
          }
          .message {
            width: auto;
            height: 30px;
            margin-left: 10px;
            color: #999;
            font-size: 12px;
            line-height: 30px;
            background: url(../../../assets/images/index/talk_16.png) no-repeat
              left center;
            padding-left: 22px;
          }
          .see {
            width: auto;
            height: 30px;
            margin-left: 50px;
            color: #999;
            font-size: 12px;
            line-height: 30px;
            background: url(../../../assets/images/index/eye_16.png) no-repeat
              left center;
            padding-left: 26px;
          }
        }
      }
    }
  }
  .post {
    position: fixed;
    z-index: 100;
    right: 0;
    top: 50%;
    .el-button {
      padding: 15px 5px;
      font-size: 16px;
    }
  }
  .wonderful {
    width: 100%;
    height: 20%;
    .wonderful-imgContent {
      width: 200px;
      height: 200px;
      display: block;
    }
    .time {
      font-size: 13px;
      color: #999;
    }
    .bottom {
      margin-top: 13px;
      line-height: 12px;
    }

    .button {
      padding: 0;
      float: right;
    }

    .image {
      width: 200px;
      height: 200px;
      display: block;
    }

    .clearfix:before,
    .clearfix:after {
      display: table;
      content: "";
    }

    .clearfix:after {
      clear: both;
    }
  }
}
</style>
