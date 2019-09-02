<template>
  <div class="pie-echart" ref="echartContainer" style="height: 250px">
  </div>
</template>

<script>
  import {debounce} from '@/utils/debounce'

  export default {
    name: 'pieEchart',
    data() {
      return {
        chart: null,
        goodsList: [],
        title: {inCircle: '60%',outCircle: '100%'},
      }
    },
    mounted() {
      this.$on('bridgePieChart', (dataList, val) => {
        this.setOptions(dataList, val)
      })
      this.initChart()
      this.__resizeHanlder = debounce(() => {
        if (this.chart) {
          this.chart.resize()
        }
      }, 100)
      window.addEventListener('resize', this.__resizeHanlder)
    },
    beforeDestroy() {
      if (!this.chart) {
        return
      }
      window.removeEventListener('resize', this.__resizeHanlder)
      this.chart.dispose()
      this.chart = null
    },
    methods: {
      initChart() {
        this.chart = echarts.init(this.$refs.echartContainer, 'macarons')
        this.setOptions(this.goodsList, this.title)
      },
      setOptions(dataList, val) {
        this.chart.setOption({
          tooltip: {
            trigger: 'item',
            formatter: '{b}: {c} ({d}%)',
            textStyle: {
              color: '#000'
            },
            backgroundColor: '#FFF',
            padding: 10
          },
          series: [
            {
              name: '',
              type: 'pie',
              radius: [val.inCircle, val.outCircle],
              avoidLabelOverlap: false,
              hoverOffset: 20,
              selectedOffset: 20,
              clockwise: true,
              startAngle: 90,
              minAngle: 10,
              minShowlabelAngle: 20,
              label: {
                show: false,
                position: 'outSide',
                emphasis: {
                  show: false,
                  textStyle: {
                    fontSize: '30',
                    fontWeight: 'bold'
                  }
                },
                fontSize: 20
              },
              labelLine: {
                show: false,
                length: 30,
                lineStyle: {
                  color: 'red',
                  width: 2
                }
              },
              itemStyle: {
                borderWidth: 10,	//边框的宽度
                borderColor: 'rgb(255,255,255)',	//边框的颜色
                emphasis: {
                  show: true,
                  borderColor: 'rgb(255,255,255)'
                }
              },
              data: dataList,
              // color: this.colorPie,
              center: ['50%', '50%']
            }
          ]
        })
      }
    }
  }
</script>

<style>

</style>
