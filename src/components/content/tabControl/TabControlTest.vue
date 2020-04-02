<template>
   <div class="table-control-test">
     <div v-for="(item,index) in titles"
          class="table-control-test-item"
          :class="{active:index===currentIndex}"
          @click="activeClick(index)"
     >
       <span>{{item}}</span>
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
      },
      data(){
          return{
            currentIndex:0
          }

      },
      methods:{
        activeClick(index){
          this.currentIndex=index;
          console.log("tabclick");
          this.$emit('tabClick',index)
        }
      }
    }
</script>

<style scoped>
.table-control-test{
  display: flex;
  justify-content: space-around;
  font-size: 15px;
  height: 40px;
  line-height: 40px;
  text-align: center;
  background-color: #fff;
}
.table-control-test-item span {
  padding: 8px;
}
.active{
  color: var(--color-high-text);
}
.active span{
  border-bottom: 3px solid var(--color-tint);
}
</style>
