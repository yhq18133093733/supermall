<template>
    <div class="recommends">
       <div v-for="(item, index) in recommends" class="recommend-item" :key="index">
         <a :href="item.link">
           <img :src="item.image">
           <div>{{item.title}}</div>
         </a>
       </div>
    </div>
</template>

<script>
    export default {
        name: "RecommendViewTest",
        props:{
          recommends:{
            type:Array,
            default(){
              return []
            }
          }
        }
    }
</script>

<style scoped>
.recommends{
  display: flex;
  justify-content: space-around;
  /*text-align: center;*/
  /*margin-bottom: 30px;*/
  padding: 10px 0px 20px 0px;
  /*background: red;*/
}
/*.recommend-item {*/
/*    flex: 1;*/
/*  }*/
  .recommends img{
    width: 70px;
    height: 70px;
    margin-bottom: 10px;
  }
</style>
