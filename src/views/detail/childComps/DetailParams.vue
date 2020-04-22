<template>
    <div class="param-info" v-if="Object.keys(itemParams).length !== 0">

        <table v-for="table in itemParams.rule.tables">
          <tr v-for="tr in table">
            <td  v-for="td in tr">{{td}}</td>
          </tr>
        </table>

       <table class="info-param">
          <tr v-for="info in itemParams.info.set">
            <td class="td-key">{{info.key}}</td>
            <td class="td-value">{{info.value}}</td>
          </tr>
        </table>

    </div>
</template>

<script>
    export default {
        name: "DetailParams",
      props:{
          itemParams:{
            type:Object
          }
      }
    }
</script>

<style scoped>
.param-info {
    padding: 20px 15px;
    font-size: 14px;
    border-bottom: 5px solid #f2f5f8;
  }

  .param-info table {
    width: 100%;
    border-collapse: collapse;
  }

  .param-info table tr {
    height: 42px;
  }

  .param-info table tr td {
    border-bottom: 1px solid rgba(100,100,100,.1);
  }
  .info-param{
    /*width: 100%;*/
  }
  .td-key{
    width: 30%;
  }
  .td-value{
    width: 70%;
    color: #eb4868;
  }
</style>
