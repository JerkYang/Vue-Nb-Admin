<template>
  <div :class="className" :id="id" :style="{height:height,width:width}"></div>
</template>

<script>
  import echarts from 'echarts'
  import resize from './mixins/resize'

  export default {
    mixins: [resize],
    props: {
      className: {
        type: String,
        default: 'chart'
      },
      id: {
        type: String,
        default: 'chart'
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
            trigger: 'axis',
            formatter: '{b}<br/>{a0}: {c0}%<br />{a1}: {c1}%<br />{a2}: {c2}%<br/>{a3}: {c3}%'
          },
          legend: {
            data: ['1#锅炉', '2#锅炉', '3#锅炉', '4#锅炉'],
            left: 'center',
            top: '1%',
            itemWidth: 40, // 图例的宽度
            itemHeight: 10, // 图例的高度
            textStyle: { // 图例文字的样式
              color: '#FFF',
              fontSize: 15
            }
          },
          toolbox: {
            show: false,
            feature: {
              dataZoom: {},
              dataView: {
                readOnly: false
              },
              magicType: {
                type: ['line', 'bar']
              },
              restore: {},
              saveAsImage: {
                pixelRatio: 5
              }
            }
          },
          xAxis: {
            type: 'category',
            name: '日期',
            nameTextStyle: {
              fontSize: '20'
            },
            axisLabel: {
              interval: 0,
              rotate: 30,
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
            data: ['2018-08-06', '2018-08-07', '2018-08-08', '2018-08-09', '2018-08-10', '2018-08-11', '2018-08-12']
          },
          yAxis: {
            type: 'value',
            // min:-35,
            name: '锅炉排污率',
            nameTextStyle: {
              fontSize: '20'
            },
            axisLabel: {
              formatter: '{value} %',
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
            min: 2,
            max: 12,
            interval: 1
          },
          series: [
            {
              name: '1#锅炉',
              type: 'line',
              smooth: true,
              itemStyle: {
                normal: {
                  color: '#ff1200'
                }
              },
              data: [7.386363636, 7.317073171, 5.076142132, 9.547738693, 3.743315508, 5.970149254, 7.692307692],
              // data: [61.63, 1.9, 2.16, 2.55, 2.7, 2.69, 2.65, 2.87, 2.9, 3.1, 3.47, 3.89, 4.54, 5.33, 5.95, 6.44, 6.94, 7.45, 7.61, 8.44, 9.35, 9.58, 10.06, 10.6, 10.94, 11.49, 11.03, 11.11],
              markPoint: {
                label: {
                  show: true,
                  formatter: '{c}%'
                },
                data: [{
                  type: 'max',
                  name: '最大值'
                },
                {
                  type: 'min',
                  name: '最小值'
                },
                {
                  coord: [41, 15],
                  name: '15',
                  value: 15
                }
                ]
              }
            },
            {
              name: '2#锅炉',
              type: 'line',
              smooth: true,
              itemStyle: {
                normal: {
                  color: '#ff8c47'
                }
              },
              data: [9.61072286, 7.504992091, 8.243866028, 6.09400301, 5.10229017, 8.92646102, 7.29380164],
              // data: [12.84, 13.03, 13.05, 13.89, 13.72, 12.97, 13.21, 14.02, 14.54, 15.07, 14.94, 14.55, 13.84, 12.7, 12.06, 11.93, 11.6, 10.84, 10.26, 10.18, 10.21, 9.86, 10.1, 9.96, 10.25, 11.1, 11.08, 10.7],
              markPoint: {
                label: {
                  show: true,
                  formatter: '{c}%'
                },
                data: [{
                  type: 'max',
                  name: '最大值'
                },
                {
                  type: 'min',
                  name: '最小值'
                },
                {
                  coord: [41, 15],
                  name: '15',
                  value: 15
                }
                ]
              }
            },
            {
              name: '3#锅炉',
              smooth: true,
              itemStyle: {
                normal: {
                  color: '#20a4b9'
                }
              },
              type: 'line',
              markPoint: {
                label: {
                  formatter: '{c}%'
                },
                data: [{
                  type: 'max',
                  name: '最大值'
                },
                {
                  type: 'min',
                  name: '最小值'
                }
                ]
              },
              data: [8.801468528, 6.436117802, 9.90293395, 4.815861515, 7.000589821, 8.18082465, 7.783040092]
              // data: [7.38, 7.73, 7.46, 7.85, 7.68, 7.45, 6.94, 6.7, 5.98, 6.25, 6.28, 5.74, 5.51, 5.35, 5.25, 5.03, 4.83, 4.57, 4.58, 4.33, 4.6, 4.42, 4.38, 3.95, 3.82, 3.7, 3.75, 3.71]
            },
            {
              name: '4#锅炉',
              type: 'line',
              smooth: true,
              itemStyle: {
                normal: {
                  color: '#82cb02'
                }
              },
              data: [7.686109758, 8.909110375, 8.031491315, 6.912127862, 10.00348259, 5.04177259, 8.307369871],
              // data: ['-', '-', 23.55, 21.24, 21.26, 21.32, 20.88, 20.23, 21.2, 20.36, 18.28, 18.93, 18.85, 19.19, 18.79, 18.1, 18.06, 17.88, 17.38, 17.06, 16.04, 15.98, 15.17, 15.17, 15.16, 14.77, 14.91, 14.76],
              markPoint: {
                label: {
                  show: true,
                  formatter: '{c}%'
                },
                data: [{
                  type: 'max',
                  name: '最大值'
                },
                {
                  type: 'min',
                  name: '最小值'
                },
                {
                  coord: [41, 15],
                  name: '15',
                  value: 15
                }
                ]
              }
            }
          ]
        })
      }
    }
  }
</script>
