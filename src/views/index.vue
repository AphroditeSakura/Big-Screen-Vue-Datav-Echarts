<template>
  <div id="index" >
    <dv-full-screen-container class="bg">
    <div class="box-container">
        <div class="box-flex">
            <dv-decoration10 style="width:40%;height:.0625rem;" />
            <dv-decoration-10 style="width:40%; height:.0625rem;transform: rotateY(180deg);"/>
        </div>
       <div class="box-flex-dir">
           <span class="title">能源管理平台</span>
       </div>
       <div class="decoration-5">
           <dv-decoration-5 style="width:30%;height:20px;dur:10;" />
       </div >
      <div class="two-box" >
          <dv-border-box-10  class="box-10" >
              <BaseLoadAChart/>
          </dv-border-box-10 >
          <dv-border-box-10 class="box-10">
              <bottomLeft />
          </dv-border-box-10>
      </div>
    </div>
    </dv-full-screen-container>
  </div>
</template>

<script>
  import BaseLoadAChart from "../components/echart/bottom/BaseLoadAChart";
  import bottomLeft from "./bottomLeft";

export default {
  data() {
    return {
      loading: true,
    };
  },
  components: {
      BaseLoadAChart,
      bottomLeft
  },
  mounted() {
    this.cancelLoading();
    // 定时刷新当前时间
    this.currentTime();
  },
  methods: {
      // eslint-disable-next-line no-unused-vars
      rollSize:function(refName){
              /* 获取当前页面的缩放比
                    若未设置zoom缩放比，则为默认100%，即1，原图大小
                */
          var zoom = parseInt(this.$refs.refName.style.zoom) || 100;
              /* event.wheelDelta 获取滚轮滚动值并将滚动值叠加给缩放比zoom
                    wheelDelta统一为±120，其中正数表示为向上滚动，负数表示向下滚动
                */
          zoom += event.wheelDelta / 12;
              /* 最小范围 和 最大范围 的图片缩放尺度 */
          if (zoom >= 100 && zoom <250) {
              this.$refs.refName.style.zoom = zoom + "%";
          }
          return false;
      },
    getTime: function () {
      var _this = this;
      let yy = new Date().getFullYear();
      let mm = new Date().getMonth() + 1;
      let dd = new Date().getDate();
      let hh = new Date().getHours();
      let mf =
        new Date().getMinutes() < 10
          ? "0" + new Date().getMinutes()
          : new Date().getMinutes();
      let ss =
        new Date().getSeconds() < 10
          ? "0" + new Date().getSeconds()
          : new Date().getSeconds();
      _this.currtime = yy + "-" + mm + "-" + dd + " " + hh + ":" + mf + ":" + ss;
    },
    currentTime() {
      setInterval(this.getTime, 500);
    },
    cancelLoading() {
      setTimeout(() => {
        this.loading = false;
      }, 500);
    },
  },
};
</script>

<style lang="scss">
    .two-box{
        display: flex;
        justify-content:space-between;
        height: 40%;
    }

    .decoration-5{
        display: flex;
        justify-content: center;
    }
    .title{
        margin: 4px;
        font-size: 20px;
        text-align: center;
    }
    .box-container{
        width: 100%;
        height: 100%;
    }
    .box-flex{
        display: flex;
        justify-content:space-between;
    }
    .box-flex-dir{
        margin: 5px;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }
    .box-10{
        width: 45%;
        height:100%;
        margin: 5px;
    }
@import "../assets/scss/index.scss";
</style>