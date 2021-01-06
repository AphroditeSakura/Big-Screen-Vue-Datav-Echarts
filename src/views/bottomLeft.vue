<template>
      <div class="bottom-left">
        <BaseTempChart  ref="BaseTempChart"/>
        <!-- <bottomLeftChartState ref="bottomLeftChartState" /> -->
      </div>
</template>

<script>
//import bottomLeftChart from "@/components/echart/bottom/bottomLeftChart";
import BaseTempChart from "@/components/echart/bottom/BaseTempChart";
// import bottomLeftChartState from "@/components/echart/bottom/bottomLeftChartState";
export default {
  data() {
    return {};
  },
  components: {
   BaseTempChart,
    // bottomLeftChartState,
  },
  mounted() {
    this.changeTiming();

  },
  methods: {
        changeTiming() {
      setInterval(() => {
        this.fetchSystemSum(); //获取-状态
      }, 3000);
    },
    async fetchSystemSum() {
      const { data } = await this.$http.get("getDataByName?name=GROUP_HAN_SUM");

      let status = data.status;
      let dataList = JSON.parse(data.data);

      if (status === 200) {
        this.$refs.BaseTempChart.refresh(dataList);
      }
    },
  },
};
</script>

<style lang="scss">
.bottom-left {
    width: 95%;
    height:80%;
    margin:20px auto ;
  }
</style>