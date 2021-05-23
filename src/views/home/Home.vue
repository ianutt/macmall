<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
<!--    <home-swiper :banners="banners"/>
    <home-recommend-view :recommends="recommends"/>
    <home-feature-view/>
    <tab-control class="tab-contral" :titles="['流行','新款','精选']" @tabClick="tabClick"/>
    <goods-list :goods="showGoods"/>-->
  </div>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar";
/*import TabControl from "@/components/content/tabControl/TabControl";

import HomeSwiper from "@/views/home/childComps/HomeSwiper";
import HomeRecommendView from "@/views/home/childComps/HomeRecommendView";
import HomeFeatureView from "@/views/home/childComps/HomeFeatureView";
import GoodsList from "@/components/content/goods/GoodsList";

import {getHomeMultidata, getHomeGoods} from "@/network/home";*/

export default {
  name: 'Home',
  components:{
    NavBar
  }
}

/*export default {
  name: "Home",
  components: {
    NavBar,
    TabControl,
    HomeSwiper,
    HomeRecommendView,
    HomeFeatureView,
    GoodsList
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: { //变量
        'pop': { page: 0, list: [] },
        'new': { page: 0, list: [] },
        'sell': { page: 0, list: [] },
      },
      currentType: 'pop'
    }
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list
    }
  },
  created() { //只写发送请求，具体的方法写在methods里面
    //1.请求多个数据
    this.getHomeMultidata()

    //2.请求商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  methods: {
    //事件监听相关方法
    tabClick(index) {
      //console.log(index);
      switch (index) {
        case 0:
          this.currentType = 'pop'
          break
        case 1:
          this.currentType = 'new'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
    },

    //网络请求相关方法
    getHomeMultidata() {
      getHomeMultidata().then( res => {
        //console.log(res); //res不要打引号，会打印字符串
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      })
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type,page ).then( res => {
        //console.log(res);
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
      })
    }
  }
}*/

</script>

<style scoped>
  #home{
    padding-top: 44px;
  }
  .home-nav{
    background: var(--color-tint);
    color: #fff;
    position: fixed;
    left: 0;
    top: 0;
    right: 0;
    z-index: 9;
  }
  .tab-contral{
    position: sticky;
    top:44px;
    background: #fff;
    z-index: 9;
  }
</style>
