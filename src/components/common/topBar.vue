<template>
    <div id="topBar">
        <div class="top-infor">
            <div class="top-infor-img">
                <img :src="seller.avatar">
            </div>
            <div class="top-infor-text">
                <h1>
                    <i class="icon iconfont icon-dianpu"></i>
                    {{seller.name}}
                </h1>
                <span>{{seller.description}}/{{seller.deliveryTime}}分钟送达</span>
                <div>
                    <i class="icon iconfont icon-tianmaozengyunfeixian"></i>
                    {{seller.supports[0].description}}
                </div>
            </div>
            <div class="top-infor-more" @click="isShowIntro = true">
                {{seller.supports.length}}个
                <i class="el-icon-arrow-right"></i>
            </div>
            <div class="top-infor-bg">
                <img :src="seller.avatar">
            </div>
        </div>
        <div class="top-public">
            <p>
                <i class="icon iconfont icon-gonggao"></i>
                <span>{{seller.bulletin}}</span>
                <i class="el-icon-arrow-right" @click="isShowIntro = true"></i>
            </p>
        </div>
        <div class="top-swiper">
            <span><router-link to="order">商品</router-link></span>
            <span><router-link to="rating">评价</router-link></span>
            <span><router-link to="shop">商家</router-link></span>
        </div>
        <div class="top-mask" v-show="isShowIntro">
            <h1>{{seller.name}}</h1>
            <el-rate v-model="seller.score" disabled>
            </el-rate>
            <div>
                <h2>优惠信息</h2>
                <ul>
                    <li v-for="(support,index) in seller.supports" :key="index">
                        <i class="icon iconfont icon-zhengpinbaozhang"></i>
                        {{support.description}}
                    </li>
                </ul>
            </div>
            <div>
                <h2>商家公告</h2>
                <p>{{seller.bulletin}}</p>
            </div>
            <span @click="isShowIntro = false"><i class="el-icon-close" style="font-size:28px"></i></span>
        </div>
        <div class="top-admin">
            <router-link to="/admin">
              <i class="icon iconfont icon-wo"></i>
            </router-link>
        </div>
    </div>
</template>
<script>
export default {
  data() {
    return {
      seller: {
        supports:[{}]
      },
      isShowIntro: false
    };
  },
  created: function() {
    this.api.getSeller()
      .then(res => {
        if(res.data.status){
          this.seller = res.data.data;
        }
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>
<style lang="less">
#topBar {
  .top-infor {
    height: 60px;
    position: relative;
    background: rgba(7, 17, 27, 0.7);
    padding: 30px 0px 20px 25px;
    color: #fff;
    .top-infor-img {
      float: left;
      margin-right: 15px;
      img {
        width: 64px;
        height: 64px;
        border-radius: 5px;
      }
    }
    .top-infor-text {
      float: left;
      h1 {
        font-size: 16px;
      }
      div {
        font-size: 10px;
      }
      span {
        font-size: 12px;
        display: block;
        margin: 10px 0px;
      }
    }
    .top-infor-more {
      height: 25px;
      width: 50px;
      position: absolute;
      top: 70px;
      left: 320px;
      background-color: rgba(0, 0, 0, 0.2);
      font-size: 12px;
      line-height: 25px;
      text-align: center;
      border-radius: 10px;
    }
    .top-infor-bg {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      img {
        height: 100%;
        width: 100%;
      }
    }
  }
  .top-public {
    background-color: #333;
    padding: 8px;
    p {
      font-size: 12px;
      color: #fff;
      span {
        width: 320px;
        height: 14px;
        line-height: 14px;
        display: inline-block;
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }
    }
  }
  .top-swiper {
    font-size: 14px;
    padding: 15px 50px;
    border-bottom: 1px solid #ccc;
    span {
      margin-right: 80px;
    }
    span:last-child {
      margin-right: 0px;
    }
  }
  .top-mask {
    color: #fff;
    background-color: #000;
    opacity: 0.8;
    position: fixed;
    min-height: 700px;
    z-index: 3;
    top: 0px;
    padding-top: 65px;
    text-align: center;
    .el-rate {
      margin: 20px 0px;
    }
    ul {
        text-align: left;
        padding: 28px 48px;
        font-size: 12px;
        li {
            margin-top: 16px;
            i {
                margin-right: 2px;
            }
        }
    }
    p {
        padding: 28px 48px;
        letter-spacing: 2px;
        text-align: left;
        font-size: 12px;
        line-height: 24px;
    }
  }
  .top-admin {
    position: absolute;
    top: 10px;
    right: 10px;
    font-size: 12px;
    font-weight: 700;
    a {
      color: #00a0dc;
    }
  }
}
</style>
