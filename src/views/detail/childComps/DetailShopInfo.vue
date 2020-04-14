<template>
    <div class="shop-info">
      <div class="logo-info">
        <img :src="shopInfo.shopLogo">
        <span class="shop-name">{{shopInfo.name}}</span>
      </div>
      <div class="shop-score">
        <div class="score-left">
          <div class="sells" style="text-align: center;">
            <div>
              {{shopInfo.cSells}}
            </div>
            <div style="font-size: 12px;padding-top: 5px">
              总销量
            </div>
          </div>
          <div class="all-goods" style="text-align: center;">
             <div>
              {{shopInfo.cGoods}}
            </div>
            <div style="font-size: 12px;padding-top: 5px">
              全部宝贝
            </div>
          </div>
        </div>
        <div class="score-right">
          <table>
          <tr v-for="(item, index) in shopInfo.score" :key="index">
            <td>{{item.name}}</td>
            <td class="score" :class="{'score-better': item.isBetter}">{{item.score}}</td>
            <td class="better" :class="{'better-more': item.isBetter}"><span>{{item.isBetter ? '高':'低'}}</span></td>
          </tr>
        </table>
        </div>
      </div>
       <div class="shop-bottom">
          <div class="enter-shop">进店逛逛</div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "DetailShopInfo",
      props:{
          shopInfo:{
            type:Object
          }
      }
    }
</script>

<style scoped>
  .shop-info{
    /*position: relative;*/
    width: 100%;
    margin-top: 20px;
    border-bottom: 3px solid #fff9ff;
  }
  .logo-info{
   display: flex;
   align-items: center;
  }
  .logo-info img{
    width: 45px;
    height: 45px;
    margin-left: 5px;
    background: #27e20b;
  }
  .shop-name{
    margin-left: 5px;
    font-size: 16px;
  }
  .shop-score{
    display: flex;
    height: 80px;
  }
  .score-left{
    width: 50%;
    display: flex;
    color: #222222;
    justify-content: space-around;
    align-items: center;
    border-right: 1px solid #c1c1c1;
  }
  .sells{

  }
  .score-right{
    width: 50%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
  }
  .better{
    color: white;
    background-color: #5ea732;
  }

  .score{
    color: #27e20b;
  }
  .score-better{
    color: #ff1955;
  }
  .better-more{
    text-align: center;
    background-color: #f13e3a;
  }
  .score-right table {
    width: 120px;
    margin-left: 30px;
  }

  .score-right table td {
    font-size: 14px;
    padding-top: 5px;
  }

  .score span{
    font-size: 14px;
  }

  .shop-bottom {
    text-align: center;
    margin-top: 10px;
  }

  .enter-shop {
    display: inline-block;
    font-size: 14px;
    background-color: #f2f5f8;
    width: 150px;
    height: 30px;
    text-align: center;
    line-height: 30px;
    border-radius: 10px;
  }
</style>
