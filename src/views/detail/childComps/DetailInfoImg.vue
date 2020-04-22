<template>
    <div v-if="Object.keys(detailInfo).length !== 0" class="goods-info">
<!--    <div v-if="detailInfo != null && detailInfo !=''" class="detail-info-img">-->
      <div class="desc-info">
      <div class="start"></div>
      <div class="desc">{{detailInfo.desc}}</div>
      <div class="end"></div>
        <div class="key">{{detailInfo.detailImage[0].key}}</div>
      </div>
      <div class="detail-img">
        <img v-for="(item,index) in detailInfo.detailImage[0].list" :src="item">
      </div>

    </div>
</template>

<script>
    export default {
        name: "DetailInfoImg",
      props:{
          detailInfo:{
            type:Object,
          }
      }
    }
</script>

<style scoped>
  .goods-info {
    padding: 20px 0;
    border-bottom: 5px solid #f2f5f8;
  }
  .desc-info{
    padding: 0 15px;
  }
  .desc{
    font-size: 14px;
    margin: 10px 0;
  }
  .start, .end{
    /*margin: 20px 0;*/
    width: 30%;
    height: 1px;
    background-color: black;
    position: relative;
  }
  .end{
    float: right;
  }
  .start:before{
    content: '';
    width: 5px;
    height: 5px;
    position: absolute;
    background-color: #222222;
    bottom: 0;
  }
  .end:after{
    content: '';
    width: 5px;
    height: 5px;
    position: absolute;
    background-color: #222222;
    right: 0;
  }
  .key{

  }
  .detail-img img{
    width: 100%;
  }
</style>
