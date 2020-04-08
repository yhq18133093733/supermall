<template>
  <swiper class="detail-swiper">
    <swiper-item v-for="(item,index) in topImg">
      <img :src="item">
    </swiper-item>
  </swiper>
</template>

<script>
  import { Swiper, SwiperItem} from 'components/common/swiper/index'
    export default {
        name: "DetailSwiper",
      props: {
        topImg: {
          type:Array,
          default(){
            return []
          }
        }
      },
      components:{
        Swiper,
        SwiperItem
      }
    }
</script>

<style scoped>
.detail-swiper{
  height: 300px;
}
</style>
