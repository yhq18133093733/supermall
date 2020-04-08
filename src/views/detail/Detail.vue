<template>
  <div>
    <detail-tab-bar></detail-tab-bar>
    <detail-swiper :topImg="detail"></detail-swiper>
  </div>
</template>

<script>
    import DetailTabBar from "./childComps/DetailTabBar";
    import DetailSwiper from "./childComps/DetailSwiper";
    import {getDetail} from "network/detail";

    export default {
        name: "Detail",
      components:{
        DetailSwiper,
          DetailTabBar
      },
      data(){
        return{
          iid:null,
          detail:[]
        }
      },
      created() {
         this.getMallDetail(this.$route.params.iid)
      },
      methods:{
          getMallDetail(iid){
            getDetail(iid).then(res =>{
              this.detail=res.result.itemInfo.topImages;
            })
          }
      }
    }
</script>

<style scoped>

</style>
