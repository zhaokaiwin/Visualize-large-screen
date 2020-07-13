<template>
  <div>
    <div id="bottomChart"></div>
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
      let myChartPieLeft = echarts.init(document.getElementById("bottomChart"));
      myChartPieLeft.resize();
      let cszlData = this.chartData.data.cszl;
      let csczl = this.chartData.data.csczl;
      let nczlData = this.chartData.data.nczl;
      let ncczl = this.chartData.data.ncczl;
      let cszl = [];
      let nczl = [];
      cszlData.forEach((el, index) => {
        cszl.push(el - csczl[index]);
      });
      nczlData.forEach((el, index) => {
        nczl.push(el - ncczl[index]);
      });
      // console.log(cszlData)
      let max = cszlData.reduce(function(a, b) {
        return b > a ? b : a;
      });

      let option = {
        legend: {
          data: ["城市总量", "城市处置量", "农村总量", "农村处置量"],
          textStyle: {
            color: "#BED7FA",
            fontSize: 12
          }
          // icon: "roundRect"
        },
        grid: {
          left: "0",
          right: "0",
          bottom: "0",
          containLabel: true
        },
        xAxis: {
          axisTick: {
            show: false
          },
          type: "category",
          axisLine: {
            lineStyle: {
              color: "#BED7FA",
              opacity: "0.1"
            }
          },
          splitLine: {
            show: false,
            lineStyle: {
              color: "#BED7FA",
              type: "dashed"
            }
          },
          data: ["南湖区", "秀洲区", "经开区"]
        },
        yAxis: [
          {
            axisTick: {
              show: false
            },
            type: "value",
            name: "单位(套)",
            min: 0,
            max: max,
            axisLine: {
              lineStyle: {
                color: "#BED7FA",
                opacity: "0"
              }
            },
            axisLabel: {
              formatter: "{value} K"
            },
            splitLine: {
              lineStyle: {
                type: "solid",
                opacity: "0.1"
              }
            }
          }
        ],
        series: [
          {
            name: "城市处置量",
            type: "bar",
            barWidth: 10,
            stack: "城市",
            color: "#04A0FE",
            data: csczl,
            itemStyle: {
              normal: {
                //柱形图圆角，初始化效果
                barBorderRadius: [0, 0, 40, 40],
                label: {
                  show: false //是否展示
                }
              }
            }
          },
          {
            name: "城市总量",
            type: "bar",
            color: "rgba(4,160,254,0.40)",
            barWidth: 10,
            stack: "城市",
            data: cszl,
            itemStyle: {
              normal: {
                //柱形图圆角，初始化效果
                barBorderRadius: [40, 40, 0, 0],
                label: {
                  show: false //是否展示
                }
              }
            }
          },

          {
            name: "农村处置量",
            type: "bar",
            barWidth: 10,
            stack: "农村",
            color: "#FCB33A",
            data: ncczl,
            grid: {
              top: "5% "
            },
            itemStyle: {
              normal: {
                //柱形图圆角，初始化效果
                barBorderRadius: [0, 0, 40, 40],
                label: {
                  show: false //是否展示
                }
              }
            }
          },
          {
            name: "农村总量",
            type: "bar",
            color: "rgba(252,179,58,0.40)",
            barWidth: 10,
            stack: "农村",
            data: nczl,
            itemStyle: {
              normal: {
                //柱形图圆角，初始化效果
                barBorderRadius: [40, 40, 0, 0],
                label: {
                  show: false //是否展示
                }
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
#bottomChart {
  width: 400px;
  height: 250px;
}
</style>