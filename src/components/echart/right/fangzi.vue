<template>
  <div>
    <div id="fdckclChart"></div>
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
      let myChartPieLeft = echarts.init(document.getElementById("fdckclChart"));
      myChartPieLeft.resize();
      let zsyts = this.chartData.aa;
      let option = {
        color: ["#2BB7FF", "#FCB33A"],
        legend: {
          data: ["商品房成交量", "二手房成交量"],
          textStyle: {
            color: "#BED7FA",
            fontSize: 12
          }
          //   icon: "roundRect"
        },
        xAxis: [
          {
            axisTick: {
              show: false
            },
            axisLine: {
              lineStyle: {
                color: "#BED7FA",
                opacity: "0.2"
              }
            },
            axisLabel: {
              // x轴数据隔一个显示
              // interval: 1
            },
            type: "category",
            boundaryGap: false,
            nameTextStyle: {
              color: "#fff"
            },
            data: [
              "2019/02",
              "2019/04",
              "2019/06",
              "2019/08",
              "2019/10",
              "2019/12"
            ]
          }
        ],
        yAxis: {
          axisTick: {
            show: false
          },
          axisLine: {
            lineStyle: {
              color: "#BED7FA",
              opacity: "0.2"
            }
          },
          min: 0,
          max: 80,
          interval: 20,
          type: "value",
          name: "数量(套)",
          //网格线
          splitLine: {
            lineStyle: {
              type: "solid",
              opacity: "0.1"
            }
          },
          axisLabel: {
            formatter: "{value} K"
          },
          nameTextStyle: {
            padding: [0, 50, 0, 0]
          }
        },
        grid: {
          left: 55
        },
        series: [
          {
            name: "商品房成交量",
            type: "line",
            symbol: "none",
            smooth: true,
            data: zsyts,
            lineStyle: {
              color: "#FCB33A"
            },
            areaStyle: {
              color: {
                type: "linear",
                x2: 0,
                y2: 1,
                colorStops: [
                  {
                    offset: 0,
                    color: "rgba(252,179,58,0.45)" // 0% 处的颜色
                  },
                  {
                    offset: 0.5,
                    color: "rgba(252,179,58,0.23)" // 100% 处的颜色
                  },
                  {
                    offset: 1,
                    color: "rgba(252,179,58,0.00)" // 100% 处的颜色
                  }
                ]
              }
            }
          },
          {
            name: "二手房成交量",
            type: "line",
            // 平滑曲线
            smooth: true,
            // 拐点样式：隐藏
            symbol: "none",
            lineStyle: {
              color: "#2BB7FF"
            },
            data: [23, 28, 23, 22, 28, 20, 22, 20, 25, 28, 20, 22, 20],
            areaStyle: {
              color: {
                type: "linear",
                x2: 0,
                y2: 1,
                colorStops: [
                  {
                    offset: 0,
                    color: "rgba(43,183,255,0.45)" // 0% 处的颜色
                  },
                  {
                    offset: 0.5,
                    color: "rgba(43,183,255,0.23)" // 100% 处的颜色
                  },
                  {
                    offset: 1,
                    color: "rgba(43,183,255,0.00)" // 100% 处的颜色
                  }
                ]
              }
            }
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
#fdckclChart {
  width: 37rem;
  height: 25.77rem;
  position: relative;
  top: 1rem;
  left: -0.3rem;
}
</style>
