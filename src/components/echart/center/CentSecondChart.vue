<template>
  <div class="center-second-chart-root">
    <div id="center-second-chart"></div>
    <span class="unit">单位(件)</span>
    <div class="label">
      <div>许可总办件量</div>
      <div style="padding-top: 0.5rem;">许可服务企业量</div>
    </div>
  </div>
</template>

<script>
const echarts = require("echarts");
export default {
  data() {
    return {
      xktotal: 0,
      xkservicecomp: 0
    };
  },
  props: ["chartData"],
  mounted() {
    this.draw();
  },
  watch: {
    chartData: {
      handler: function() {
        this.draw();
      },
      deep: true
    }
  },
  methods: {
    draw() {
      // 基于准备好的dom，初始化echarts实例
      let myChartPieLeft = echarts.init(
        document.getElementById("center-second-chart")
      );
      if (this.chartData) {
        this.xktotal = this.chartData.xktotal
          ? this.chartData.xktotal
          : 0;
        this.xkservicecomp = this.chartData
          .xkservicecomp
          ? this.chartData.xkservicecomp
          : 0;
      }
      let option = {
        color: [
          "rgba(3, 73, 169, 0.1)",
          "#60BFB9",
          "#2BB7FF"
        ],
        series: [
          {
            name: "访问来源",
            type: "pie",
            // selectedMode: "single",
            selected: {
              another: false,
              another1: false
            },
            radius: ["50%", "60%"],
            label: {
              show: false
            },
            data: [
              {
                name: "another",
                value: 100 - this.xkservicecomp
              }, 
              {
                name: "another3",
                value: this.xkservicecomp
              }
            ]
          },
          {
            name: "访问来源",
            type: "pie",
            radius: ["70%", "80%"],
            // selectedMode: "single",
            selected: {
              another: false,
              another1: false
            },
            label: {
              show: false
            },
            data: [
              { name: "another", value: 100 - this.xktotal },
              { name: "another4", value: this.xktotal }
            ]
          }
        ]
      };

      myChartPieLeft.setOption(option);
    }
  },
  destroyed() {
    window.onresize = null;
  }
};
</script>

<style lang="scss" scoped>
.center-second-chart-root {
  position: relative;

  #center-second-chart {
    width: 16rem;
    height: 16rem;
    margin-top: 0.5rem;
  }

  .unit {
    position: absolute;
    top: 7.5rem;
    left: 8.5rem;
    opacity: 0.6;
    font-family: PingFangSC-Regular;
    font-size: 0.9rem;
    color: #bed7fa;
    letter-spacing: 0;
  }
  .label {
    position: absolute;
    top: 1.9rem;
    left: 10.5rem;
    opacity: 0.6;
    font-family: PingFangSC-Regular;
    font-size: 0.9rem;
    // color: #bed7fa;
    color:white;
    letter-spacing: 0;
  }
}
</style>
