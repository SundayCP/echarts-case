<template>
  <el-container>
    <el-header>
      <div>小豚物联大数据中心</div>
      <div class="now-time">{{dateTime | dateformat('YYYY-MM-DD HH:mm:ss')}}</div>
    </el-header>
    <el-main>
      <div class="el-main-con">
        <el-col :span="12" style="background-color: #FFF;">
          <div class="grid-content">
            <header class="grid-section">
              <div>
                <div class="title">总库存量</div>
                <div class="total-num">
                  <count-to
                    :start-val="1526263" :end-val="12321" :duration="20000000000" class="card-panel-num"
                  />
                  件
                </div>
              </div>
              <div>
                <div class="title">今日出库量</div>
                <div class="total-num">
                  <count-to
                    :start-val="1000" :end-val="10000" :duration="200000000" class="card-panel-num"
                  />
                  件
                </div>
              </div>
              <div>
                <div class="title">销售总额</div>
                <div class="total-num">
                  <count-to
                    :start-val="todayNum" :end-val="searchUserCount" :duration="10000000000" class="card-panel-num"
                  />
                  元
                </div>
              </div>
            </header>
            <main>
              <div><span class="block-txt">实时出库</span></div>
              <div ref="echartContainer1" class="grid-row-three-echart"></div>
            </main>
          </div>
        </el-col>
        <el-col :span="12" style="background-color: #FFF;position: relative" class="map-area">
          <div class="grid-content bg-purple-light">
            <div><span class="block-txt">用户区域分布</span></div>
            <china-map :style="{height: '500px', width: '860px'}"/>
            <!--<ul class="china-map-legend">-->
            <!--<li>-->
            <!--<div class="color-div"></div>-->
            <!--<div class="legend-disc">大于300元</div>-->
            <!--<div>8%</div>-->
            <!--</li>-->
            <!--<li>-->
            <!--<div class="color-div"></div>-->
            <!--<div class="legend-disc">201~300元</div>-->
            <!--<div>21%</div>-->
            <!--</li>-->
            <!--<li>-->
            <!--<div class="color-div"></div>-->
            <!--<div class="legend-disc">101-200元</div>-->
            <!--<div>32%</div>-->
            <!--</li>-->
            <!--<li>-->
            <!--<div class="color-div"></div>-->
            <!--<div class="legend-disc">小于100元</div>-->
            <!--<div>39%</div>-->
            <!--</li>-->
            <!--</ul>-->
          </div>
        </el-col>
      </div>
      <div class="el-main-con" style="margin-top: 20px;">
        <el-col :span="6" style=" width: 23%; background-color: #FFF;">
          <div class="grid-content bg-purple" style="padding: 20px;">
            <div><span class="block-txt">行业分布</span>
              <el-row>
                <el-col :span="8" style="position: relative">
                  <div class="pie-text">
                    <div style="font-size: 14px">服装行业</div>
                    <div style="text-align: center;color: #000">57%</div>
                  </div>
                  <pie-chart ref="inWarehouseData1"/>
                </el-col>
                <el-col :span="8" style="position: relative">
                  <div class="pie-text">
                    <div style="font-size: 14px">医疗器械</div>
                    <div style="text-align: center;color: #000">21%</div>
                  </div>
                  <pie-chart ref="inWarehouseData2"/>
                </el-col>
                <el-col :span="8" style="position: relative">
                  <div class="pie-text">
                    <div style="font-size: 14px">其它</div>
                    <div style="text-align: center;color: #000">12%</div>
                  </div>
                  <pie-chart ref="inWarehouseData3"/>
                </el-col>
              </el-row>
            </div>
          </div>
        </el-col>
        <el-col :span="6" style=" width: 23%; background-color: #FFF;">
          <div class="grid-content bg-purple-light" style="padding: 20px;">
            <div><span class="block-txt">门店销售排名</span></div>
            <div style="height: 250px;padding: 0 10px;">
              <ranking-list v-model="storeSaleList"></ranking-list>
            </div>
          </div>
        </el-col>
        <el-col :span="6" style=" width: 23%; background-color: #FFF;">
          <div class="grid-content bg-purple" style="padding: 20px;">
            <div><span class="block-txt">热销商品</span></div>
            <div ref="echartContainer10" style=" width: 100%; height: 250px; padding: 15px;"></div>
          </div>
        </el-col>
        <el-col :span="6" style=" width: 23%; background-color: #FFF;">
          <div class="grid-content bg-purple-light" style="padding: 20px;">
            <div><span class="block-txt">支付方式分布</span></div>
            <div style="display: flex;align-items: center">
              <div style="position: relative;width: 65%">
                <div class="pie-text">
                  <div style="font-size: 14px;text-align: center">{{textTitle}}</div>
                  <div style="text-align: center;color: #000">{{val5}}</div>
                </div>
                <pie-chart ref="inWarehouseData4"/>
              </div>
              <div style=" width: 35%">
                <div style="margin-bottom: 5px"><span
                  style="background-color:rgb(59, 161, 255);display:inline-block;width: 10px;height: 10px;border-radius: 50%"></span><span>&nbsp;&nbsp;微信</span>&nbsp;&nbsp;&nbsp;&nbsp;<span
                  style="color: gray">{{(val1/(val1+val2+val3+val4)*100).toFixed(2)}}%</span></div>
                <div style="margin-bottom: 5px"><span
                  style="background-color:rgb(79, 203, 116);display:inline-block;width: 10px;height: 10px;border-radius: 50%"></span><span>&nbsp;&nbsp;支付宝</span>&nbsp;&nbsp;&nbsp;&nbsp;<span
                  style="color: gray">{{(val2/(val1+val2+val3+val4)*100).toFixed(1)}}%</span></div>
                <div style="margin-bottom: 5px"><span
                  style="background-color:rgb(251, 212, 56);display:inline-block;width: 10px;height: 10px;border-radius: 50%"></span><span>&nbsp;&nbsp;会员</span>&nbsp;&nbsp;&nbsp;&nbsp;<span
                  style="color: gray">{{(val3/(val1+val2+val3+val4)*100).toFixed(2)}}%</span></div>
                <div style="margin-bottom: 5px"><span
                  style="background-color:rgb(240, 72, 100);display:inline-block;width: 10px;height: 10px;border-radius: 50%"></span><span>&nbsp;&nbsp;现金</span>&nbsp;&nbsp;&nbsp;&nbsp;<span
                  style="color: gray">{{(val4/(val1+val2+val3+val4)*100).toFixed(2)}}%</span></div>
              </div>
            </div>
          </div>
        </el-col>
      </div>
    </el-main>
  </el-container>
</template>

<script>
  import {debounce} from '@/utils/debounce'
  import CountTo from 'vue-count-to'
  import ChinaMap from './components/ChinaMap'
  import PieChart from './components/pieEchart'
  import RankingList from './components/rankingList'

  export default {
    name: 'index',
    components: {CountTo, ChinaMap, PieChart, RankingList},
    data () {
      return {
        dateTime: new Date(),
        totalNum: 123213,
        searchUserCount: 15262634,

        todayNum: 5554545,
        saleMoney: 656453424,
        stock: {
          dataList: {
            dataValue: [50, 35, 60, 40, 20, 25, 28, 35, 40, 30, 15, 20],
            dataLine: ['16:23:20', '16:24:20', '16:25:20', '16:26:20', '16:27:20', '16:28:20', '16:29:20', '16:30:20', '16:31:20', '16:32:20', '16:33:20', '16:34:20']
          },
        },
        myChart1: null,
        myChart10: null,
        num: 10,
        val1: 0,
        val2: 0,
        val3: 0,
        val4: 0,
        textTitle: '',
        val5: 0,
        dataCon:[
          {value: 10, name: '宽松百搭上衣T恤ins洋气'},
          {value: 20, name: '新款韩版潮流半袖'},
          {value: 15, name: '麻棉宽腿七分裤'},
          {value: 25, name: '2019新款潮流夏季冰丝夏装'},
          {value: 20, name: '2019新款韩版学生'},
          {value: 35, name: 'AIRism防紫外线拉链连帽开衫'},
          {value: 30, name: '夏季新款潮牌条纹修身海魂衫'},
          {value: 40, name: '夏季潮流薄款中裤'}
        ],

        storeSaleList: [
          {
            roleName: 'AIRism防紫外线网眼...',
            totalAmount: 23425,
          },
          {
            roleName: '2019新款短袖t恤女...',
            totalAmount: 38366,
          },
          {
            roleName: 'cec上衣服纯棉白色T恤...',
            totalAmount: 39423,
          },
          {
            roleName: '紧身纯白色T恤女短袖...',
            totalAmount: 40025,
          },
          {
            roleName: 'MFRC-522 RFID...',
            totalAmount: 41316,
          },
        ],

        dataPieCharts1: [
          {
            name: '萧山新湾分销商',  //名称
            value: 1446.80,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(58, 161, 254)'}  //各版块的颜色
          },
          {
            name: '还是分销商',  //名称
            value: 1046.80,  // 所占比的值
            rate: '60.00%',  // 所占百分比
            price: 500, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(240, 242, 245)'}  //各版块的颜色
          },
        ],

        dataPieCharts2: [
          {
            name: '萧山新湾分销商',  //名称
            value: 300.80,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(106, 210, 136)'}  //各版块的颜色
          },
          {
            name: '还是分销商',  //名称
            value: 1046.80,  // 所占比的值
            rate: '60.00%',  // 所占百分比
            price: 500, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(240, 242, 245)'}  //各版块的颜色
          },
        ],

        dataPieCharts3: [
          {
            name: '萧山新湾分销商',  //名称
            value: 100.80,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(252, 219, 86)'}  //各版块的颜色
          },
          {
            name: '还是分销商',  //名称
            value: 1046.80,  // 所占比的值
            rate: '60.00%',  // 所占百分比
            price: 500, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(240, 242, 245)'}  //各版块的颜色
          },
        ],

        dataPieCharts4: [
          {
            name: '萧山新湾分销商',  //名称
            value: 1500.80,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(59, 161, 255)'}  //各版块的颜色
          },
          {
            name: '萧山新湾分销商',  //名称
            value: 500.80,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(79, 203, 116)'}  //各版块的颜色
          },
          {
            name: '萧山新湾分销商',  //名称
            value: 500.80,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(251, 212, 56)'}  //各版块的颜色
          },
          {
            name: '还是分销商',  //名称
            value: 246.80,  // 所占比的值
            rate: '60.00%',  // 所占百分比
            price: 500, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(240, 72, 100)'}  //各版块的颜色
          },
        ]
      }
    },
    filters: {
      toThousands (nStr) {
        nStr += ''
        let x = nStr.split('.')
        let x1 = x[0]
        let x2 = x.length > 1 ? '.' + x[1] : ''
        var rgx = /(\d+)(\d{3})/
        while (rgx.test(x1)) {
          x1 = x1.replace(rgx, '$1' + ',' + '$2')
        }
        return x1 + x2
      }
      ,
      toThousands2 (num) {
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
    }
    ,
    mounted () {
      this.$refs.inWarehouseData1.$emit('bridgePieChart', this.dataPieCharts1, {inCircle: '60%', outCircle: '100%'})
      this.$refs.inWarehouseData2.$emit('bridgePieChart', this.dataPieCharts2, {inCircle: '60%', outCircle: '100%'})
      this.$refs.inWarehouseData3.$emit('bridgePieChart', this.dataPieCharts3, {inCircle: '60%', outCircle: '100%'})
      this.$refs.inWarehouseData4.$emit('bridgePieChart', this.dataPieCharts4, {inCircle: '45%', outCircle: '80%'})
      let _this = this
      this.timer = setInterval(() => {
        _this.dateTime = new Date()
      }, 1000)

      this.timer2 = setInterval(() => {
        this.num++

        let val = this.num * Math.random(0.6, 0.8) * 10

        // new Date()
        let t = new Date().getHours() + ':' + new Date().getMinutes() + ':' + new Date().getSeconds()

        this.stock.dataList.dataValue.shift()
        this.stock.dataList.dataLine.shift()

        this.stock.dataList.dataValue.push(val)
        this.stock.dataList.dataLine.push(t)

      }, 5000)

      this.timer3 = setInterval(() => {
        this.num++

        let hh = this.dataCon.shift()
        this.dataCon.push(hh)

        this.val1 = this.num * Math.random(0.9, 1) * 100
        this.val2 = this.num * Math.random(0.9, 1) * 100
        this.val3 = this.num * Math.random(0.9, 1) * 100
        this.val4 = this.num * Math.random(0.9, 1) * 100

        // let ss = ['服装行业','医疗器械','其它']
        let s = ['服装行业', '医疗器械', '其它']
        this.textTitle = s[this.num % 3]
        this.val5 = (this.num * Math.random(0.9, 1) * 1000).toFixed(2)

        this.dataPieCharts4 = [
          {
            name: '萧山新湾分销商',  //名称
            value: this.val1,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(59, 161, 255)'}  //各版块的颜色
          },
          {
            name: '萧山新湾分销商',  //名称
            value: this.val2,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(79, 203, 116)'}  //各版块的颜色
          },
          {
            name: '萧山新湾分销商',  //名称
            value: this.val3,  // 所占比的值
            rate: '150.00%',  // 所占百分比
            price: 100, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(251, 212, 56)'}  //各版块的颜色
          },
          {
            name: '还是分销商',  //名称
            value: this.val4,  // 所占比的值
            rate: '60.00%',  // 所占百分比
            price: 500, // 对应的金额
            totalCount: 2000, //对应的数量
            itemStyle: {color: 'rgb(240, 72, 100)'}  //各版块的颜色
          },
        ]

      }, 5000)

      this.getEchartsLine()
      this.getEchartsPie()

      this.__resizeHanlder = debounce(() => {
        if (this.myChart1 && this.myChart10) {
          this.myChart1.resize()
          this.myChart10.resize()
        }
      }, 100)
      window.addEventListener('resize', this.__resizeHanlder)
    }
    ,
    updated () {
      this.$refs.inWarehouseData4.$emit('bridgePieChart', this.dataPieCharts4, {inCircle: '45%', outCircle: '80%'})
      this.getEchartsLine()
      this.getEchartsPie()

      // this.$refs.inWarehouseData1.$emit('bridgePieChart', this.dataPieCharts1,{inCircle: '60%',outCircle: '100%'})
      // this.$refs.inWarehouseData2.$emit('bridgePieChart', this.dataPieCharts2,{inCircle: '60%',outCircle: '100%'})
      // this.$refs.inWarehouseData3.$emit('bridgePieChart', this.dataPieCharts3,{inCircle: '60%',outCircle: '100%'})
      // this.$refs.inWarehouseData4.$emit('bridgePieChart', this.dataPieCharts4,{inCircle: '50%',outCircle: '80%'})
    }
    ,
    beforeDestroy () {
      if (this.timer) {
        clearInterval(this.timer)
      }
      if (this.timer2) {
        clearInterval(this.timer2)
      }
      if (this.timer3) {
        clearInterval(this.timer3)
      }
      if (!this.myChart1 && !this.myChart10) {
        return
      }
      window.removeEventListener('resize', this.__resizeHanlder)
      this.myChart1.dispose()
      this.myChart10.dispose()
      this.myChart1 = null
      this.myChart10 = null
    }
    ,
    methods: {
      //头部折线图
      getEchartsLine () {
        this.myChart1 = echarts.init(this.$refs.echartContainer1)// 初始化echarts实例
        this.myChart1.setOption({
          title: {text: 'ECharts'},
          tooltip: {
            show: true,
            trigger: 'axis',
            // formatter: "{a} <br/>{b}: {c} ({d}%)"
          },
          xAxis: {
            data: this.stock.dataList.dataLine,
            // name: '日期',
            boundaryGap: false,
            nameLocation: 'end',
            nameTextStyle: {
              padding: [20, 0, 0, 0],
              color: 'red',
              fontWeight: 'normal',
              fontSize: 16
            },
            nameGap: '10',
            nameRotate: 0,
            axisLine: {
              symbol: 'none',
              show: true,
              lineStyle: {
                color: 'gray',
                width: 1,
              },
              symbolSize: [10, 15],
              symbolOffset: [-10, 10]
            },
            axisTick: {
              alignWithLabel: true,
              show: true,
              inside: true,
              length: 5,
              lineStyle: {
                color: 'gray',
                width: 0,
                type: 'solid'
              }
            },
            axisLabel: {
              color: '#000',
              rotate: 0,
              show: true,
              inside: false,
            },
          },
          yAxis: {
            type: 'value',
            show: true,
            axisLine: {
              show: true,
              lineStyle: {
                color: 'gray'
              }
            },
            splitLine: {
              show: false,
              lineStyle: {
                color: 'red',
                type: 'dotted'
              }
            },
            axisTick: {
              alignWithLabel: true,
              show: true,
              inside: true,
              length: 0,
              lineStyle: {
                color: 'red',
                width: 5,
                type: 'dotted'
              }
            },
            axisLabel: {
              color: '#000',
              rotate: 0,
              show: true
            },
            splitLine: {
              show: true,
            }
          },
          series: [{
            name: '销量',
            type: 'line',
            data: this.stock.dataList.dataValue,
            label: {
              show: false,
              position: 'top',
              distance: 10,
              rotate: 30,
              color: '#000',
              fontSize: 14
            },
            areaStyle: {
              color: {
                type: 'linear',
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                colorStops: [{
                  offset: 0, color: 'rgb(251, 182, 121)' // 0% 处的颜色
                }, {
                  offset: 1, color: 'rgb(251, 135, 160)' // 100% 处的颜色
                }],
                global: false // 缺省为 false
              }
            },
            itemStyle: {
              borderColor: 'rgb(254, 94, 130)',
              borderWidth: 0,
              opacity: 0
            },
            lineStyle: {
              color: 'rgb(254, 94, 130)',
              width: 1
            },
            emphasis: {
              label: false,
              itemStyle: {
                color: '#1890FF',
                borderColor: '#1890FF'
              }
            },
            smooth: 0.5
          }],
          title: {
            show: false
          },
          grid: {
            left: '1%',
            right: '5%',
            height: 'auto',
            width: 'auto',
            bottom: '5%',
            top: '6%',
            containLabel: true,
            backgroundColor: '#000'
          }
        })
      }
      ,
      getEchartsPie () {

        this.myChart10 = echarts.init(this.$refs.echartContainer10)// 初始化echarts实例
        console.log(this.myChart10)
        this.myChart10.setOption({
          title: {
            text: '',
            subtext: '',
            x: 'center'
          },
          tooltip: {
            trigger: 'item',
            formatter: '{a} <br/>{b} : {c} ({d}%)'
          },

          toolbox: {
            show: true,
            feature: {
              mark: {show: true},
              dataView: {show: true, readOnly: false},
              magicType: {
                show: true,
                type: ['pie', 'funnel']
              },
              restore: {show: true},
              saveAsImage: {show: true}
            }
          },
          calculable: true,
          series: [
            {
              name: '',
              type: 'pie',
              radius: [30, 100],
              center: ['50%', '50%'],
              roseType: 'area',
              data: this.dataCon,
            }
          ]

        })
      }
    }
  }
</script>

<style scoped lang="scss">
  .el-header {
    height: 60px;
    line-height: 60px;
    font-size: 32px;
    background-color: #fff;
    font-weight: 700;
    display: flex;
    justify-content: space-between;
    .now-time {
      font-size: 18px;
      font-weight: normal;
    }
  }

  .el-main {
    padding: 0px !important;
    margin: 20px;
    .el-col-12 {
      width: 48% !important;
    }
    .el-main-con {
      display: flex;
      justify-content: space-around;
      .grid-content {
        padding: 20px 40px;
        .grid-section {
          margin-bottom: 15px;
          display: flex;
          justify-content: space-between;
          .title {
            margin-bottom: 10px;
            font-size: 18px;
            color: darkgray;
          }
          .total-num {
            font-size: 30px;
            font-weight: 700;
          }
        }
        .block-txt {
          display: inline-block;
          padding: 0 5px;
          font-weight: 700;
          position: relative;
        }
        .block-txt:before {
          content: '';
          position: absolute;
          width: 3px;
          top: 10%;
          bottom: 10%;
          background-color: rgb(0, 121, 254);
          left: -8%;
        }
        .grid-row-three-echart {
          width: 100%;
          height: 400px;
          padding: 15px;
        }
        .pie-text {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          color: darkgray
        }
      }
      .map-area {
        ul.china-map-legend {
          position: absolute;
          font-size: 14px;
          bottom: 5%;
          left: 3%;
          li {
            height: 30px;
            display: flex;
            list-style: none;
            align-items: center;
            div {
              margin: 0 8px;
            }
            .color-div {
              width: 10px;
              height: 10px;
              border-radius: 10px;
            }
            .legend-disc {
              width: 80px;
            }
            &:nth-child(1) {
              .color-div {
                background-color: #1920AC;
              }
            }
            &:nth-child(2) {
              .color-div {
                background-color: #3D46E2;
              }
            }
            &:nth-child(3) {
              .color-div {
                background-color: #6A71FF;
              }
            }
            &:nth-child(4) {
              .color-div {
                background-color: #AECDFF;
              }
            }
          }
        }
      }
    }

  }

</style>
