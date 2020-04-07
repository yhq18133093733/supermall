<template>
  <swiper>
   <!--    加 :key  不然会有warning-->
    <swiper-item v-for="(item, index) in banners" :key="index">
      <a :href="item.link">
        <img :src="item.image" alt="" @load="imageLoad">
      </a>
    </swiper-item>
  </swiper>
</template>

<script>
  import {Swiper, SwiperItem} from 'components/common/swiper'

  export default {
    name: "HomeSwiper",
    props: {
      banners: {
        type: Array,
        default() {
          return []
        }
      }
    },
    data(){
      return{
        onceLoad:false
      }

    },
    components: {
      Swiper,
      SwiperItem
    },
    methods:{
     imageLoad(){
       if (!this.onceLoad){
         this.$emit('swiperLoaded')
         this.onceLoad = true
       }
     }
    }
  }
</script>

<style scoped>

</style>
