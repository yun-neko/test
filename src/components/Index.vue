<template>
<div>
<!-- 顶部 -->
<div class="home_top">
      <div class="top_left">
        <table class="first_tb">
          <tr>
            <td>
              <a href="#">关注</a>
            </td>
            <td>
              <a href="#">下载APP</a>
            </td>
          </tr>
        </table>
      </div>

      <div class="top_right">
        <table>
          <tr>
            <!-- 修改跳转登录注册页面 -->
            <td>
              <a href="#" @click="tolog">登录 </a>
              <span class="xiegang"> / </span>
              <a href="#"> 注册</a>
            </td>
            <td>
              <a href="#">收藏</a>
            </td>
            <td>
              <a href="#" @click="toURL">购物车</a>
            </td>
            <td>
              <a href="#">公告</a>
            </td>
          </tr>
        </table>
      </div>
    </div>


      <div class="search_ui">
      <!-- 参考自https://semantic-ui.com/modules/search.html的Local Search -->
      <div class="ui search">
        <div class="ui icon input">
          <input class="prompt" type="text" placeholder="Goods what you want" />
          <i class="search icon"></i>
        </div>
        <div class="results"></div>
      </div>
    </div>
  <div class="container">
    
<!--    <div class="swiper-bg"-->
<!--         :style="{backgroundColor:slidesColor[index]}">-->
<!--    </div>-->
    <div class="stage">
      <ul class="category-nav">
        <li
          v-for="(item, index) in navbars"
          :key="index"
          class="cate-nav-item">
          <i class="cate-nav-icon" :class="item.icon"></i>
          {{item.text}}
        </li>
      </ul>
      <!-- 轮播图 -->
      <div class="swiper">
        <Swiper :slides="slidesImage" v-model="index"></Swiper>
      </div>

    </div>

    <!-- 精品推荐 -->
    <div class="rec-banner">
      <h1 class="banner-title">精品推荐</h1>
      <ul class="rec-list">
        <li
          class="rec-card"
          v-for="(item,index) in goods"
          :key="index"
          v-if="index < 3"
          @click="togglePage(item)">
          <img :src="item.cover" class="rec-media" />
          <div class="rec-profile">
            <h4>{{item.text}}</h4>
            <p class="rec-params">
              原价：<span class="rec-price">¥{{item.price}}</span>
              促销价：<span class="rec-online-price">¥{{item.onlinePrice}}</span>
            </p>
          </div>
        </li>
      </ul>
    </div>
        
    <!-- 商品促销 -->
    <div class="rec-banner">
      <h1 class="banner-title">商品促销</h1>
      <ul class="rec-list">
        <li
          class="rec-card"
          v-for="(item,index) in goods"
          :key="index"
          v-if="index > 3"
          @click="togglePage(item)">
          <img :src="item.cover" class="rec-media" />
          <div class="rec-profile">
            <h4>{{item.text}}</h4>
            <p class="rec-params">
              原价：<span class="rec-price">¥{{item.price}}</span>
              促销价：<span class="rec-online-price">¥{{item.onlinePrice}}</span>
            </p>
          </div>
        </li>
      </ul>
    </div>


    <!-- 部分页面没功能 -->
    <div class="recommand2">
      <table>
        <tr>
          <td colspan="3"><h2>今日主推大牌</h2></td>
        </tr>

        <!-- 待考虑添加，做切换 -->
        <tr>
          <td colspan="3"></td>
        </tr>
        <tr>
          <td class="re_pic">
            <img src="../../icons/recommand/recommand4.jpg" width="100%" />
          </td>
          <td class="re_pic">
            <img src="../../icons/recommand/recommand5.jpg" width="100%" />
          </td>
          <td class="re_pic">
            <img src="../../icons/recommand/recommand6.jpg" width="100%" />
          </td>
        </tr>
      </table>
      <table class="recommand2">
        <tr>
          <td><i class="big angle left icon"></i></td>

          <td><img src="../../icons/recommand/logo.jpg" /></td>
          <td><img src="../../icons/recommand/logo2.jpg" /></td>
          <td><img src="../../icons/recommand/logo3.jpg" /></td>
          <td><img src="../../icons/recommand/logo4.jpg" /></td>
          <td><img src="../../icons/recommand/logo5.jpg" /></td>

          <td><i class="big angle right icon"></i></td>
        </tr>
      </table>
    </div>


    
  </div>


  <!-- 底部 -->
  <div class="home_end">
        <div class="end_table">

        
        <table>
            <tr>
                <td>正品保证</td>
                <td>十天退货</td>
                <td>十天调补差价额</td>
                <td colspan="3">09:00~21:00在线客服</td>
            </tr>
            <tr>
                <td>新手帮助</td>
                <td>购物指南</td>
                <td>支付/配送</td>
                <td>售后服务</td>
                <td>会员服务</td>
                <td>优购客服</td>
            </tr>
            <tr>
                <td><img src="../../icons/end/end1.jpg" alt="#"></td>
                <td><img src="../../icons/end/end2.jpg" alt="#"></td>
                <td><img src="../../icons/end/end3.jpg" alt="#"></td>
                <td colspan="3"></td>

            </tr>
            <tr>
                <td>关于优购 |</td>
                <td>集团采购 |</td>
                <td>招贤纳士 |</td>
                <td>手机优购 |</td>
                <td>联系我们 |</td>
                <td>友情链接</td>
            </tr>
           
            <tr>
                <td colspan="6">
                    Copyright © 2011-2016 Yougou Technology Co., Ltd. 粤ICP备09070608号 深公网安备：4403101910665 粤公网安备 44030502000017号
                </td>
            </tr>
        </table>
        </div>
    </div>


  </div>
</template>

<script>
  import Swiper from '@/widgets/Swiper'
  import config from '@/config/config'
  export default {
    name: "Index",
    components: {Swiper},
    data() {
      return{
        index:0
      }
    },
    computed: {
      navbars () {
        return config.navbars
      },
      goods () {
        return config.goods
      },
      // slidesColor () {
      //   return config.goods.map(item => item.color)
      // },
      slidesImage () {
        return config.goods.map(item => item.poster)
      }
    },
    methods: {
      togglePage (item) {
        this.$router.push({path: 'goods', query: { name: item.name}})
      },
      toURL(){
        this.$router.push({
          path:'cart'
        })
      },
      tolog(){
        this.$router.push({
          path:'loginout'
        })
      }
    }
  }
</script>

<style scoped>

/* 顶部 */
.home_top {
  position: relative;
  margin: 0 auto;
  width: 100%;
  height: 40px;
  background-color: black;
}

a {
  color: white;
  text-decoration: none;
}

a:hover {
  color: #eb4500;
}

.first_tb {
  position: fixed;
  left: 40px;
}

td {
  padding: 0;
  line-height: 40px;
  width: 90px;
}

.top_right {
  position: fixed;
  right: 20px;
}

.xiegang {
  color: grey;
}

.search_ui{
  height: 40px;
}

  .container {
    position: relative;
    background-color: #f5f5f5;
    border-bottom: 1px solid transparent;
  }
  .swiper-bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 500px;
    background-color: #e5e5e5;
  }
  .stage {
    width: 1120px;
    margin-left: auto;
    margin-right: auto;
    background-color: #789;
  }
  .category-nav {
    /*display: inline-block;*/
    position: absolute;
    width: 200px;
    height: 500px;
    z-index: 2;
    list-style: none;
    background-color: rgba(0, 0, 0, 0.55);
    margin-top: 0px;
  }
  .cate-nav-item {
    padding-left: 12px;
    line-height: 35.7143px;
    color: #fff;
    cursor: pointer;
  }
  .cate-nav-item:hover {
    color: #787878;
    background-color: rgba(255, 255, 255, .8);
  }
  .cate-nav-icon {
    opacity: .5;
  }
  .swiper {
    height: 500px;
    background-color: #e8e8e8;
  }
  .rec-banner {
    margin: 30px auto;
    padding-top: 30px;
    padding-bottom: 50px;
    width: 1120px;
    background-color: #fff;
  }
  .banner-title {
    padding: 8px 15px;
  }
  .rec-list {
    list-style: none;
  }
  .rec-card {
    display: inline-block;
    width: 25%;
    text-align: center;
    vertical-align: top;
    cursor: pointer;
  }
  .rec-media {
    width: 240px;
  }
  .rec-profile {
    width: 200px;
    display: inline-block;
    color: #444;
  }
  .rec-price {
    text-decoration: line-through;
  }
  .rec-online-price {
    color: #ff0036;
    font-size: 16px;
  }
  .rec-params {
    font-size: 12px;
    color: #888;
  }

/* 推荐 */
.recommand2 {
  width: 950px;
  margin: 0 auto;
  text-align: center;
}

.re_pic {
  width: 315px;
  height: 402px;
}

/* 底部样式 */
  .home_end {
    background-color: black;
    color: white;
}

.end_table{
    width: 950px;
    margin: 0 auto;
}
</style>
