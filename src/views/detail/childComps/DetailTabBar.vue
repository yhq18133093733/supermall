<template>
  <div>
    <nav-bar >
      <img slot="left" class="imgLeft" @click="back" src="~assets/img/common/back.svg" alt="">
      <div slot="center" class="topBar">
        <div v-for="(item,index) in detailTitle"
        :class="{active:currentIndex === index}"
        @click="itemClick(index)"
        >
          {{item}}
        </div>
      </div>
    </nav-bar>
  </div>
</template>

<script>
  import NavBar from "components/common/navbar/NavBar";
    export default {
        name: "DetailTabBar",
      components:{
          NavBar
      },
       data(){
          return{
            detailTitle:['商品', '参数', '评论', '推荐'],
            currentIndex:0
          }
      },
      methods: {
        itemClick(index) {
          this.currentIndex = index
        },
        back(){
          this.$router.back();
        }
      }
    }
</script>

<style scoped>
.topBar{
  display: flex;
  justify-content: space-around;
  font-size: 15px;
}
  .imgLeft{
    margin-top: 12px;
  }
  .active{
    color: red;
  }
</style>
