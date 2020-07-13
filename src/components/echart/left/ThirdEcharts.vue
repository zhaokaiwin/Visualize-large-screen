<template>
  <div>
    <div id="left-third-chart"></div>
  </div>
</template>

<script>
const echarts = require("echarts");
export default {
  data() {
    return {};
  },
  props: ["rdata"],
  mounted() {
    this.draw();
  },
  watch: {
    rdata: {
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
        document.getElementById("left-third-chart")
      );
      let xAxisData = this.rdata.xAxisData;
      let seriesData = this.rdata.seriesData;
      
      let option = {
        xAxis: {
          data: xAxisData,
          axisTick: { show: true },
          axisLine: { show: true },
          axisLabel: {
            color: " #BED7FA"
          }
        },
        yAxis: {
          splitLine: { show: true },
          axisTick: { show: true },
          axisLine: { show: true },
          axisLabel: { show: true, color: "#BED7FA" }
        },
        grid: {
          left: 0,
          top: 10,
          right: 0,
          bottom: 0,
          containLabel: true
        },
        color: ["#00BFFF"],
        series: [
          {
            name: "hill",
            type: "pictorialBar",
            barCategoryGap: "-50%",
            // symbol: 'path://M0,10 L10,10 L5,0 L0,10 z',
            symbol:
              "path://M0,10 L10,10 C5.5,10 5.5,5 5,0 C4.5,5 4.5,10 0,10 z",
            itemStyle: {
              opacity: 0.5
            },
            emphasis: {
              itemStyle: {
                opacity: 1
              }
            },
            data: seriesData,
            z: 10
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
#left-third-chart {
  width: 32rem;
  height: 15rem;
  margin-top: 0.5rem;
}
</style>