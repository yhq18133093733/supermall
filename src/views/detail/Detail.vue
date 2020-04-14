<template>
  <div class="detail">
    <detail-tab-bar></detail-tab-bar>
    <scroll class="contain">
      <detail-swiper :topImg="detail"></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shopInfo="shopInfo"></detail-shop-info>
      <div>1</div>
      <div>1</div>
      <div>1</div>
      <div>1</div>
      <div>1</div>
      <div>1</div>
      <div>1</div>
      <div>1</div>
      <div>1</div>
      <div>1</div>
    </scroll>

  </div>
</template>

<script>
    import DetailTabBar from "./childComps/DetailTabBar";
    import DetailSwiper from "./childComps/DetailSwiper";
    import DetailBaseInfo from "./childComps/DetailBaseInfo";
    import DetailShopInfo from "./childComps/DetailShopInfo";

    import scroll from 'better-scroll'
    import {getDetail,Goods} from "network/detail";
    import Scroll from "../../components/common/scroll/Scroll";

    export default {
        name: "Detail",
      components:{
        DetailShopInfo,
        Scroll,
        DetailBaseInfo,
        DetailSwiper,
          DetailTabBar
      },
      data(){
        return{
          iid:null,
          detail:[],
          goods:{},
          shopInfo:{}
        }
      },
      created() {
         this.getMallDetail(this.$route.params.iid)
      },
      methods:{
          getMallDetail(iid){
            getDetail(iid).then(res =>{
              this.detail=res.result.itemInfo.topImages;
              this.goods=new Goods(res.result.itemInfo,res.result.columns,res.result.shopInfo.services)
              this.shopInfo=res.result.shopInfo
              console.log(this.shopInfo);
            })
          }
      }
    }
</script>

<style scoped>
  .contain{
    height: calc(100% - 44px);
  }
.detail{
  background-color: #fff;
  position: relative;
  height: 100vh;
  z-index: 1;
}
</style>
