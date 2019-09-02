<template>
  <div class="header-ranking-list">
    <div class="grid-content3-contain-right-title" >{{title}}</div>
    <div style="color:rgba(0,0,0,0.65);" v-if="storeSaleList.length > 0">
      <div class="grid-content3-contain-right-list" style="    background-color:rgb(250, 250, 250);">
        <div class="grid-content3-contain-right-list-num" style="font-weight: 700">排名</div>
        <div class="grid-content3-contain-right-list-store" style="font-weight: 700">SKU</div>
        <div class="grid-content3-contain-right-list-price" style="font-weight: 700">库存数量</div>
      </div>
      <div class="grid-content3-contain-right-list" v-for="(item,index) in storeSaleList" :key="index">
        <div class="grid-content3-contain-right-list-num">{{index+1}}</div>
        <div class="grid-content3-contain-right-list-store">{{item.roleName}}</div>
        <div class="grid-content3-contain-right-list-price">{{item.totalAmount}}</div>
      </div>
    </div>
    <div v-else>
      <div style="text-align: center">暂无数据</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'rankingList',
    model: {prop: 'storeSaleList'},
    props:{
      storeSaleList:{
        type: Array,
        default:[],
      },
      title:{
        type:String,
        default: '',
      },

    },
    filters: {
      toThousands(num) {
        var num1 = Number(num).toFixed(2).split('.')[0]
        var num2 = Number(num).toFixed(2).split('.')[1]
        var num3 = (num1 || 0).toString(), result = ''
        while (num3.length > 3) {
          result = ',' + num3.slice(-3) + result
          num3 = num3.slice(0, num3.length - 3)
        }
        if (num3) {
          result = num3 + result
        }
        if (typeof num2 !== 'undefined') {
          result = result + '.' + num2
        }
        return result
      }
    },

  }
</script>

<style lang="scss">
  .header-ranking-list {
    .grid-content3-contain-right-title {
      margin-bottom: 24px;
      color: rgba(0, 0, 0, 0.85);
      font-size: 14px;
      font-weight: 700;
      font-family:PingFangSC-Medium;
    }
    .grid-content3-contain-right-list {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 18px;
      .grid-content3-contain-right-list-num {
        width: 20px;
        height: 20px;
        background-color: rgba(240, 242, 245, 1);
        text-align: center;
        line-height: 20px;
        border-radius: 50%;
        color: rgba(0, 0, 0, 0.65);

      }
      .grid-content3-contain-right-list-store {
        width: 50%;
      }
      .grid-content3-contain-right-list-price {
        text-align: right;
      }
    }

    .grid-content3-contain-right-list:nth-child(1) {
      .grid-content3-contain-right-list-num{
        /*background-color:rgb(49, 70, 89);*/
        border-radius: unset;
        background-color: unset;
        /*color: #FFF;*/
        width: unset;
        height: unset;
        padding: 0 10px 0 2px;
      }
    }
    .grid-content3-contain-right-list:nth-child(2) {
      .grid-content3-contain-right-list-num{
        background-color: rgb(49, 70, 89);
        color: #FFF;
      }
    }
    .grid-content3-contain-right-list:nth-child(3) {
      .grid-content3-contain-right-list-num{
        background-color:rgb(49, 70, 89);
        color: #FFF;
      }
    }
    .grid-content3-contain-right-list:nth-child(4) {
      .grid-content3-contain-right-list-num{
        background-color:rgb(49, 70, 89);
        color: #FFF;
      }
    }
  }
</style>
