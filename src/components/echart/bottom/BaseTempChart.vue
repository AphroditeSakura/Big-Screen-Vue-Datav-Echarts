<template>

    <div id="base-temp-chart" class="temp"></div>
</template>

<script>
import echartMixins from "@/utils/resizeMixins";
export default {
  data() {
    return {
      chart: null,
    };
  },
  mixins: [echartMixins],
  mounted() {
    this.draw();
  },
  methods: {
    // eslint-disable-next-line no-unused-vars
    refresh(data) {
      let option = this.chart.getOption();

      this.chart.setOption(option);
    },
    draw() {
      // 基于准备好的dom，初始化echarts实例
      this.chart = this.$echarts.init(document.getElementById("base-temp-chart",)
      ,"dark");

      let option = {
        title: {
          text: ''
        },
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data:["供水温度","回水温度"]},
        toolbox: {
          show: true,
          feature: {
            magicType: { type: ['line', 'bar'] }
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['0:00', '0:30', '1:00', '1:30', '2:00', '2:30','3:00',
            '3:30', '4:00','4:30', '5:00', '5:30','6:00', '6:30', '7:00',
            '7:30', '8:00', '8:30','9:00', '9:30', '10:00','10:30', '11:00',
            '11:30','12:00', '12:30','13:00', '13:30', '14:00', '14:30', '15:00',
            '15:30','16:00', '16:30', '17:00','17:30', '18:00', '18:30','19:00', '19:30',
            '20:00', '20:30', '21:00', '21:30','22:00', '22:30', '23:00','23:30', '24:00',
          ]
        },
        yAxis: {
            name:'温度',
            type: 'value',
            axisLabel: {
                formatter: '{value} °C'
          }
        },
        series: [
          {
            name: '供水温度',
            type: 'line',
            data: [10, 11, 13, 11, 12, 12, 9,10, 11, 13, 11, 12, 12, 9,10, 11, 13, 11,
              12, 12, 9,10, 11, 13, 11, 12, 12, 9,10, 11, 13, 11, 12, 12, 9,10, 11, 13,
              11, 12, 12, 9],
            markLine: {
              data:[
                      { type: 'average', name: '供水日平均温度' }
              ]
            }
          },
          {
            name: '回水温度',
            type: 'line',
            data: [1, -2, 2, 5, 3, 2, 0,1, -2, 2, 5, 3, 2, 0,1, -2, 2, 5, 3, 2, 0,1,
              -2, 2, 5, 3, 2, 0,1, -2, 2, 5, 3, 2, 0,1, -2, 2, 5, 3, 2, 0,1, -2, 2,
              5, 3, 2, 0],
            markLine: {
              data: [
                { type: 'average', name: '回水日平均温度' },
                [
                  {
                    symbol: 'none',
                    x: '90%',
                    yAxis: 'max'
                  },
                  {
                    symbol: 'circle',
                    label: {
                      position: 'start',
                      formatter: '最高温度'
                    }
                  }
                ]
              ]
            }
          }
        ]
      }
      this.chart.setOption(option);
    },
  },
  destroyed() {
    window.onresize = null;
  },
};
</script>

<style lang="scss" scoped>
  .temp{
    width: 100%;
    height:100%;
    overflow: hidden;
  }
</style>