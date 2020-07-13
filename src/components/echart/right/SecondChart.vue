<template>
  <div>
    <div id="right-second-chart"></div>
  </div>
</template>

<script>
const echarts = require("echarts");
export default {
  data() {
    return {};
  },
  props: ["chartData"],
  watch: {
    chartData: {
      handler: function() {
        this.draw();
      },
      deep: true
    }
  },
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      // 基于准备好的dom，初始化echarts实例
      let myChartPieLeft = echarts.init(
        document.getElementById("right-second-chart")
      );
      let xAxisData = this.chartData.xAxisData;
      let seriesData = this.chartData.seriesData;
      // let citynums = seriesData.citynums;
      // let citystartworknum = seriesData.citystartworknum;
      // let cityendworknum = seriesData.cityendworknum;
      let villagenums = seriesData.villagenums;
      let villagestartworknum = seriesData.villagestartworknum;
      let villageendworknum = seriesData.villageendworknum;

      let option = {
        legend: {
          data: ["城市总量", "城市开工数量", "城市完工数量", "农村总量", "农村开工数量","农村完工数量"],
          top: 10,
          icon: "rect",
          itemWidth: 10,
          itemHeight: 10,
          textStyle: {
            color: " #BED7FA"
          }
        },
        grid: {
          left: 0,
          right: 0,
          bottom: 0,
          top: 45,
          containLabel: true
        },
        xAxis: [
          {
            type: "category",
            data: xAxisData,
            axisLabel: {
              color: " #BED7FA",
              interval: 0,
              rotate: 45
            }
          }
        ],
        yAxis: [
          {
            type: "value",
            axisLabel: {
              color: " #BED7FA"
            }
          }
        ],
        series: [
          // {
          //   name: "城市总量",
          //   type: "bar",
          //   stack: "1",
          //   itemStyle: {
          //     color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          //       { offset: 0, color: "rgba(217, 79, 100, 0.4)" },
          //       { offset: 1, color: "rgba(217, 79, 100, 0.0)" }
          //     ])
          //   },
          //   data: citynums
          // },
          // {
          //   name: "城市处置量",
          //   type: "bar",
          //   stack: "1",
          //   itemStyle: {
          //     color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          //       { offset: 0, color: "#D94F64" },
          //       { offset: 1, color: "rgba(217, 79, 100, 0.0)" }
          //     ])
          //   },
          //   data: citystartworknum
          // },
          // {
          //   name: "城市处置量1",
          //   type: "bar",
          //   stack: "1",
          //   itemStyle: {
          //     color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          //       { offset: 0, color: "#D94F64" },
          //       { offset: 1, color: "rgba(217, 79, 100, 0.0)" }
          //     ])
          //   },
          //   data: cityendworknum
          // },
          {
            name: "农村总量",
            type: "bar",
            stack: "2",
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: "rgba(43, 183, 255, 0.4)" },
                { offset: 1, color: "rgba(43, 183, 255, 0.0)" }
              ])
            },
            data: villagenums
          },
          {
            name: "农村开工数量",
            type: "bar",
            stack: "2",
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: "#2BB7FF" },
                { offset: 1, color: "rgba(43, 183, 255, 0.0)" }
              ])
            },
            data: villagestartworknum
          },
          {
            name: "农村完工数量",
            type: "bar",
            stack: "2",
            itemStyle: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
                { offset: 0, color: "#D94F64" },
                { offset: 1, color: "rgba(217, 79, 100, 0.0)" }
              ])
            },
            data: villageendworknum
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
#right-second-chart {
  width: 32rem;
  height: 20rem;
  margin-top: 0.5rem;
}
</style>