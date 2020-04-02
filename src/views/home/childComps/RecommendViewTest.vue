<template>
  <div class="recommends">
    <div v-for="(item,index) in recommends" class="recommends-item">
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
  width: 100%;
  justify-content: space-around;
  font-size: 15px;

  padding: 10px 0 20px;
  border-bottom: 10px solid #eee;
}
.recommends-item{
  text-align: center;
}
  .recommends img{
    height: 75px;
    width: 75px;
    margin-top: 5px;
    margin-bottom: 5px;
  }
</style>
