<template>
    <div class="tabControl">
       <div v-for="(item,index) in titles" class="tabControl-item">
         <div>{{item}}</div>
       </div>
    </div>
</template>

<script>
    export default {
        name: "TabControlTest",
        props:{
          titles: {
            type:Array,
            default(){
              return []
            }
          }
        }
    }
</script>

<style scoped>
.tabControl{
  display: flex;
  text-align: center;
  width: 100%;
}
  .tabControl-item{
    flex: 1;
  }
</style>
