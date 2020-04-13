<template>
  <div>
    <detail-tab-bar></detail-tab-bar>
    <detail-swiper :topImg="detail"></detail-swiper>
    <detail-base-info :goods="goods"></detail-base-info>
  </div>
</template>

<script>
    import DetailTabBar from "./childComps/DetailTabBar";
    import DetailSwiper from "./childComps/DetailSwiper";
    import DetailBaseInfo from "./childComps/DetailBaseInfo";
    import {getDetail,Goods} from "network/detail";

    export default {
        name: "Detail",
      components:{
        DetailBaseInfo,
        DetailSwiper,
          DetailTabBar
      },
      data(){
        return{
          iid:null,
          detail:[],
          goods:{}
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
              console.log(this.goods);
            })
          }
      }
    }
</script>

<style scoped>

</style>
