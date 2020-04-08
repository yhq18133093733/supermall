<template>
  <div id="home" class="wrapper">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <tab-control-test
                   :titles="['流行', '新款', '精选']"
                   ref="contentTabTop"
                   @tabClick="tabClick"
                   class="tab-control"
                   v-show="tabcontrol"
                   />
    <scroll class="content"
            ref="scroll"
            :probe-type="3"
            @scroll="contentScroll"
            :pull-up-load="true"
            @pullingUp="loadMore"
    >
      <home-swiper :banners="banners" @swiperLoaded="swiperLoaded"/>
      <recommend-view-test :recommends="recommends"/>
      <feature-view/>
      <tab-control-test
                   :titles="['流行', '新款', '精选']"
                   ref="contentTab"
                   @tabClick="tabClick"
                   />
      <good-list :goods="showGoods"/>
    </scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop"/>
  </div>
</template>

<script>
  //测试回滚
  //测试回滚222
  import HomeSwiper from './childComps/HomeSwiper'
  import RecommendView from './childComps/RecommendView'
  import RecommendViewTest from './childComps/RecommendViewTest'
  import FeatureView from './childComps/FeatureView'

  import NavBar from 'components/common/navbar/NavBar'
  import TabControl from 'components/content/tabControl/TabControl'
  import TabControlTest from 'components/content/tabControl/TabControlTest'
  import GoodList from 'components/content/goods/GoodsList'
  import Scroll from 'components/common/scroll/Scroll'
  import BackTop from 'components/content/backTop/BackTop'

  import { getHomeMultidata, getHomeGoods } from "network/home"

  export default {
    name: "Home",
    components: {
      HomeSwiper,
      RecommendView,
      RecommendViewTest,
      FeatureView,
      NavBar,
      TabControl,
      TabControlTest,
      GoodList,
      Scroll,
      BackTop
    },
    data() {
      return {
        banners: [],
        recommends: [],
        goods: {
          'pop': {page: 0, list: []},
          'new': {page: 0, list: []},
          'sell': {page: 0, list: []},
        },
        currentType: 'pop',
        isShowBackTop: false,
        tabcontrol:false,
        offsetTopL:0,
        saveY:0
      }
    },
    computed: {
      showGoods() {
        return this.goods[this.currentType].list
      }
    },
    created() {
      // 1.请求多个数据
      this.getHomeMultidata()

      // 2.请求商品数据
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')
    },
    mounted() {
      const refresh = this.debounce(this.$refs.scroll.refreshed,50);
      this.$bus.$on('imgLoading', () =>{
        // this.$refs.scroll &&  this.debounce(this.$refs.scroll.refreshed,50)
        // 这里不能直接this.debounce，因为这样只会执行debounce,获得返回函数，而不会执行返回的函数
        this.$refs.scroll && refresh()
      })
    },
    activated() {
      this.$refs.scroll.scrollTo(0, this.saveY, 0)
      this.$refs.scroll.refreshed()
    },
    deactivated() {
      this.saveY = this.$refs.scroll.scrollY
    },
    methods: {
      //计算contentTab离顶部的距离
      swiperLoaded(){
        this.offsetTopL=this.$refs.contentTab.$el.offsetTop;
        this.$refs.scroll.refreshed()
      },
      //防抖函数，减少请求次数
      debounce(func,delayTime){
        let timer = null;
        return function (...args) {
          // console.log(timer);
          if (timer)clearTimeout(timer)
          timer = setTimeout( () =>{
            func.apply(this,args)
          },delayTime)
        }
      },

      /**
       * 事件监听相关的方法
       */
      tabClick(index) {
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

          this.$refs.contentTab.currentIndex=index
          this.$refs.contentTabTop.currentIndex=index

      },
      backClick() {
        this.$refs.scroll.scrollTo(0, 0)
      },
      contentScroll(position) {
        this.isShowBackTop = (-position.y) > 1000
        this.tabcontrol=(-position.y) > this.offsetTopL
      },
      loadMore() {
        this.getHomeGoods(this.currentType);
        this.$refs.scroll.refreshed();
      },
      /**
       * 网络请求相关的方法
       */
      getHomeMultidata() {
        getHomeMultidata().then(res => {
          // this.result = res;
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getHomeGoods(type) {
        this.goods[type].page += 1
        getHomeGoods(type, this.goods[type].page).then(res => {
          this.goods[type].list.push(...res.data.list)
          this.$refs.scroll.finishPullUp();
        })
      }
    }
  }
</script>

<style scoped>
  #home {
    /*padding-top: 44px;*/
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background-color: var(--color-tint);
    color: #fff;

    /*position: fixed;*/
    /*left: 0;*/
    /*right: 0;*/
    /*top: 0;*/
    /*z-index: 9;*/
  }

  .tab-control {
    position: sticky;
    top: 44px;
    z-index: 9;
  }

  .content {
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }

  /*.content {*/
    /*height: calc(100% - 93px);*/
    /*overflow: hidden;*/
    /*margin-top: 44px;*/
  /*}*/
</style>
