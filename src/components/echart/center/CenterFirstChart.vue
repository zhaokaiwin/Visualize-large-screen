<template>
  <div>
    <div id="center-first-chart"></div>
  </div>
</template>

<script>
const echarts = require("echarts");
export default {
  data() {
    return {};
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
      let xAxisData = this.chartData.xAxisData;
      let house = this.chartData.seriesData.house;
      let business = this.chartData.seriesData.business;
      let office = this.chartData.seriesData.office;
      let other = this.chartData.seriesData.other;
      let seriesData = [house, business, office, other];
      let myChartPieLeft = echarts.init(
        document.getElementById("center-first-chart")
      );
      let option = {
        legend: {
          data: ["住宅", "商业", "办公", "其他"],
          icon:'rect',
          itemWidth: 10,
          itemHeight: 10,
          textStyle: {
            color: " #BED7FA"
          }
        },
        color: ["#D94F64", "#FCB33A", "#60BFB9", "#2BB7FF"],
        grid: {
          left: 0,
          right: "7%",
          bottom: 0,
          top: 45,
          containLabel: true
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: xAxisData,
          axisLabel: {
            color: " #BED7FA"
          }
        },
        yAxis: {
          type: "value",
          axisLabel: {
            color: " #BED7FA"
          }
        },
        series: seriesData
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
#center-first-chart {
  width: 23rem;
  height: 18.5rem;
  margin-top: 0.5rem;
}
</style>