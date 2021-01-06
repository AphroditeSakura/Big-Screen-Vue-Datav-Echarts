<template>
  <div>
    <div id="base-header-chart"  class=""></div>
  </div>
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
    refresh(data) {
      let option = this.chart.getOption();
      let yearList =  new Array()
      let monthList =  new Array();
      let presentDate =new Date();
      let presentYear=presentDate.getFullYear();
      for (let index = 0; index < 5; index++) {
        let elementYear = presentYear;
        yearList.unshift(elementYear);
        elementYear=elementYear-1;
      }
        for (let index = 0; index < 12; index++) {
          let elementMonth =12;
          monthList.unshift(elementMonth);
          elementMonth=elementMonth-1;
      }
        data.forEach(()=>{

        })
      option.legend.data=yearList;
      option.xAxis.data = monthList;
      this.chart.setOption(option);
    },
    draw() {
      // 基于准备好的dom，初始化echarts实例
      this.chart = this.$echarts.init(
        document.getElementById("base-header-chart")
      );
      //  ----------------------------------------------------------------
      let category = [
      ];
      let allData = [
      ];
      let hanData = [
      ];
      let rateData = [];
      for (let i = 0; i < 33; i++) {
        let rate = hanData[i] / allData[i];
        rateData[i] = rate.toFixed(2);
      }

      let option = {
        title: {
          text: "",
          x: "center",
          y: 0,
          textStyle: {
            color: "#B4B4B4",
            fontSize: 16,
            fontWeight: "normal",
          },
        },
        tooltip: {
          trigger: "axis",
          backgroundColor: "rgba(255,255,255,0.1)",
          axisPointer: {
            type: "shadow",
            label: {
              show: true,
              backgroundColor: "#7B7DDC",
            },
          },
        },
        legend: {
          textStyle: {
            color: "#B4B4B4",
          },
          top: "0%",
        },
        grid: {
          x: "8%",
          width: "88%",
          y: "4%",
        },
        xAxis: {
          data: category,
          axisLine: {
            lineStyle: {
              color: "#B4B4B4",
            },
          },
          axisTick: {
            show: true,
          },
        },
        yAxis: [
          {
            splitLine: { show: false },
            axisLine: {
              lineStyle: {
                color: "#B4B4B4",
              },
            },

            axisLabel: {
              formatter: "{value} RT",
            },
          },
          {
            splitLine: { show: false },
            axisLine: {
              lineStyle: {
                color: "#B4B4B4",
              },
            },
            axisLabel: {
              formatter: "{value} ",
            },
          },
        ],
        series: [
          {
            name: "各年份同期冷量占比",
            type: "line",
            smooth: true,
            showAllSymbol: true,
            symbol: "emptyCircle",
            symbolSize: 8,
            yAxisIndex: 1,
            itemStyle: {
              normal: {
                color: "#F02FC2",
              },
            },
            data: rateData,
          },

          {
            name: "已分配",
            type: "bar",
            barWidth: 10,
            itemStyle: {
              normal: {
                barBorderRadius: 5,
                color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: "#956FD4" },
                  { offset: 1, color: "#3EACE5" },
                ]),
              },
            },
            data: hanData,
          },

          {
            name: "代表提出",
            type: "bar",
            barGap: "-100%",
            barWidth: 10,
            itemStyle: {
              normal: {
                barBorderRadius: 5,
                color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: "rgba(156,107,211,0.8)" },
                  { offset: 0.2, color: "rgba(156,107,211,0.5)" },
                  { offset: 1, color: "rgba(156,107,211,0.2)" },
                ]),
              },
            },
            z: -12,

            data: allData,
          },
        ],
      };
      this.chart.setOption(option);
    },
  },
  destroyed() {
    window.onresize = null;
  },
};
</script>

<style lang="scss" scoped>
  .
</style>