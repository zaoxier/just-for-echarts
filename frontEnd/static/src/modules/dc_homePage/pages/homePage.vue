<template>
  <div class="homePage">
    <div class="tab-title">  
    <el-tabs v-model="activeName" >
      <el-tab-pane  v-for="(item,index) in tabList" :key="index" :label="item.hp_thirTitle" :name="item.index" >
        <el-breadcrumb separator-class="el-icon-arrow-right">
          <el-breadcrumb-item :to="{ path: '/' }">{{homeTitle.websiteName}}</el-breadcrumb-item>
          <el-breadcrumb-item>{{homeTitle.personalCenter}}</el-breadcrumb-item>
          <el-breadcrumb-item>{{item.hp_thirTitle}}</el-breadcrumb-item>
          <el-breadcrumb-item>{{item.hp_fourTitle}}</el-breadcrumb-item>
        </el-breadcrumb>
        <div class="content" v-if="index==0">
          <div class="headinfo">
            <div class="head-box">
              <img src="../../../assets/images/bg1.jpg">
            </div>
            <p class="nickname">zaozao</p>
            <div class="grade">
              <span><img src="">铜级</span>
              <span>积分：</span>
            </div>
            <p><el-button type="primary" icon="el-icon-edit"></el-button></p>
          </div>
          <div class="left">
               <div class="fanFocus">
              <div class="fanFocus--child">
                    <a href="#"><span>关注</span></a>
                    <a href="#"><span>2</span></a>
              </div>
                <div class="fanFocus--child">
                <a href="#"><span>粉丝</span></a>
                  <a href="#"><span>0</span></a>
                </a>
              </div>
              </div>  
            <el-tabs :tab-position="tabPosition" type="card" @tabs-click="handleClick">
              <el-tab-pane label="他的动态"></el-tab-pane>
              <el-tab-pane label="他的相册"><div class="main"></div></el-tab-pane>
              <el-tab-pane label="他的论坛"></el-tab-pane>
              <el-tab-pane label="他的好友"><friend-fan></friend-fan></el-tab-pane>
              <el-tab-pane label="他的资料"></el-tab-pane>
            </el-tabs>
          </div>
          <!-- <div class="main">
            <moves></moves>
            <friend-fan></friend-fan>
          </div> -->
        </div>
      </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script>
import moves from '../components/moves.vue'
import friendFan from '../components/friendFan.vue'

export default {
  name: 'homePage_index',
  data() {
    return {
      activeName: 'first',
      homeTitle: {
        websiteName: '衣着搭配',
        personalCenter: '个人中心'
      },
      tabList: [
        {
          index: 'first',
          hp_thirTitle: '我的主页',
          hp_fourTitle: '我的动态'
        },
        {
          index: 'second',
          hp_thirTitle: '设置',
          hp_fourTitle: '基本信息'
        }
      ],
      tabPosition: "left"
      // moves: false
    }
  },
  components: {
    moves,
    friendFan
  },
  methods: {
    handleClick: function(tab, event) {
      console.log(event + event.target.getAttribute('id'))
    }
  }
}
</script>

<style lang="less">
.homePage {
  .tab-title {
      margin-left: 100px;
  }
  .content{
    margin: 0 100px;
    width: 1200px;
      .headinfo{
        position: relative;
        margin-top: 100px;
        padding-top: 75px;
        height: 100px;
        border: 1px solid #e0e0e0;
        .head-box{
          width: 150px;
          height: 150px;
          margin-left: -75px;
          position: absolute;
          left: 50%;
          top: -75px;
          img{
            width: 100%;
            height: 100%;
            border-radius: 50%;
          }
        }
        p{
          text-align: center;
        }
        .nickname{
          font-size: 18px;
          font-weight: bold;
        }
        .grade{
          height: 20px;
          margin: 5px 0 10px;
          text-align: center;
        }
        .el-icon-edit:before {
          // content: "\E61C";
          background-color: #fff;
              content: "\E611";
        }
    }
    .left{
      float: left;
      margin-top: 20px;
      width: 240px;
        .fanFocus{
          width: 100%;
          padding-top: 10px;
          border-top: 2px #999 solid;
          border-left: 1px solid #e4e7ed;
          border-right: 1px solid #e4e7ed;
          border-bottom: 1px solid #e4e7ed;
          display: flex;
          position: relative;
          .fanFocus--child{
            // 
            flex: 1;
            text-align: center;
            font-size: 16px;
            &:first-child{
              &:after{
                   content: '';
    width: 1px;
    height: 50px;
    position: absolute;
    left: 50%;
    top: 10px;
    background: #e0e0e0;
              }
            }            
            span{
              display: block;
              margin-bottom: 5px;
              height: 25px;
            }
            a{
              color: #5f686b;
               &:hover{
              text-decoration: underline;
              color: #409EFF;
            }
            }
          }
        }
        .el-tabs{

               margin-top: 10px;
            .el-tabs__item.is-left{
                 width: 240px;
       text-align: center;
       &:first-child{
          // border-right: 2px solid #e4e7ed;
          border-top: 2px #999 solid;
      }
     }
        }
   
      .is-active{
        border-right-color: #e4e7ed;
      }
    }
      .main{
        width: 940px;
        padding-left: 10px;
        float: left;
            margin-top: 20px;
        .el-tabs__item{
          font-size: 16px;
        }
      }
  }
}
</style>



