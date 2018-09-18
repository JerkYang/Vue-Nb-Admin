<template>
  <div :class="className" :id="id" :style="{height:height,width:width}"></div>
</template>

<script>
  import echarts from 'echarts'
  import resize from './mixins/resize'

  export default {
    name: 'glYzq',
    mixins: [resize],
    props: {
      className: {
        type: String,
        default: 'chart'
      },
      id: {
        type: String,
        default: 'glysl'
      },
      width: {
        type: String,
        default: '200px'
      },
      height: {
        type: String,
        default: '200px'
      }
    },
    data() {
      return {
        chart: null
      }
    },
    mounted() {
      this.initChart()
    },
    beforeDestroy() {
      if (!this.chart) {
        return
      }
      this.chart.dispose()
      this.chart = null
    },
    methods: {
      initChart() {
        this.chart = echarts.init(document.getElementById(this.id))
        this.chart.setOption({
          backgroundColor: '#272e38',
          tooltip: {
            trigger: 'axis'
          },
          legend: {
            data: ['锅炉用蒸汽量'],
            left: 'center',
            top: '5%',
            itemWidth: 40, // 图例的宽度
            itemHeight: 10, // 图例的高度
            textStyle: { // 图例文字的样式
              color: '#FFF',
              fontSize: 20
            }
          },
          grid: {
            left: '0%',
            right: '3%',
            top: '22%',
            bottom: '10%',
            containLabel: true
          },
          toolbox: {
            feature: {
              saveAsImage: {}
            }
          },

          xAxis: {
            type: 'category',
            boundaryGap: false,
            axisLabel: {
              interval: 0,
              rotate: 40,
              show: true,
              textStyle: {
                color: '#FFF',
                fontSize: '10'
              }
            },
            axisLine: {
              lineStyle: {
                color: '#0087ED',
                width: 3 // 这里是为了突出显示加上的
              }
            },
            data: ['2018-08-06', '2018-08-07', '2018-08-08', '2018-08-09', '2018-08-10', '2018-08-11', '2018-08-12']
          },
          yAxis: {
            name: '吨(t)',
            nameTextStyle: {
              fontSize: '20'
            },
            type: 'value',
            splitLine: {
              show: false
            },
            axisLabel: {
              show: true,
              textStyle: {
                color: '#FFF',
                fontSize: '20'
              }
            },
            axisLine: {
              lineStyle: {
                color: '#0087ED',
                width: 3 // 这里是为了突出显示加上的
              }
            },
            min: 8.5,
            max: 13.5,
            interval: 1
          },
          series: [{
            name: '锅炉用蒸汽量',
            color: ['#1ac52e'],
            type: 'line',
            itemStyle: {
              normal: {
                lineStyle: {
                  width: 5 // 折线宽度
                },
                color: new echarts.graphic.LinearGradient(0, 0, 1, 0, [{
                  offset: 1,
                  color: '#2bc5f2' // 0% 处的颜色
                }, {
                  offset: 0,
                  color: '#1ec23d' // 100% 处的颜色
                }], false),
                opacity: 0.4
              }
            },
            data: [11.55, 11.46, 11.21, 11.70, 10.94, 9.11, 9.72]

          }]
        })
      }
    }
  }
</script>
