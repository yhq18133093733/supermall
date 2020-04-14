<template>
    <div v-if="goods.columns != null" class="base-info">
        <div class="goods-title">
            {{goods.title}}
        </div>
      <div class="price-info">
        <span class="nInfo">{{goods.newPrice}}</span>
        <span class="oInfo">{{goods.oldPrice}}</span>
        <span class="dInfo">{{goods.discount}}</span>
      </div>
      <div class="base-columns">
        <span class="sell">{{goods.columns[0]}}</span>
        <span class="collect">{{goods.columns[1]}}</span>
        <span class="deliver-time">{{goods.services[goods.services.length-1].name}}</span>
      </div>
      <div class="shopInfo-services">
        <span v-for="(item,index) in goods.services" v-if="index < goods.services.length-1" >
          <img :src="item.icon">
          {{item.name}}
        </span>
      </div>
    </div>
</template>

<script>
    export default {
        name: "DetailBaseInfo",
      props:{
          goods:{
            type:Object,
            default(){
              return ''
            }
          }
      }
    }
</script>

<style scoped>
  .base-info{
    margin-top: 10px;
    padding: 0 8px;
    color: #999;
    width: 100%;
    border-bottom: 5px solid #f2f5f8;
  }
.goods-title{
  color: #222;
  margin-top: 20px;
}
  .price-info{
    margin-top: 15px;
  }
  .nInfo{
    color: #ff1955;
    font-size: 24px;
  }
  .oInfo{
    font-size: 12px;
    margin-left: 5px;
    text-decoration:line-through
  }
  .dInfo{
    font-size: 12px;
    color: white;
    margin-left: 5px;
    background-color: #ff1955;
    border-radius: 8px;
    padding: 2px 5px;
    position: relative;
    top: -8px;
  }

  .base-columns{
    display: flex;
    margin-top: 10px;
    font-size: 12px;
    line-height: 30px;
    justify-content: space-between;
    border-bottom: 1px solid #55a1ff;
  }
  .shopInfo-services{
    display: flex;
    justify-content: space-between;
    margin-top: 5px;
    color: black;
    font-size: 13px;
    line-height: 60px;
  }
  .shopInfo-services img{
    height: 13px;
    width: 13px;
    position: relative;
    top: 2px;
    right: -3px;
  }
</style>
