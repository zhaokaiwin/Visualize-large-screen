<template>
  <div id="center1">
    <div id="center-map">
      <!--建筑业产值  -->
      <div class="left">
        <div class="title">
          建筑业产值（元）
          <span
            :class="[
              { 'is-data-up': isConstructionUp },
              { 'is-data-down': !isConstructionUp }
            ]"
            style="margin-left: 7rem;"
          >
            同比
            <span v-if="constructionData.cumulativetotalvalueyear >= 0">↑</span>
            <span v-else>↓</span>
            {{ constructionData.cumulativetotalvalueyear }}%
          </span>
        </div>
        <div class="building color">{{ constructionData.cumulativetotalvalue }}</div>
      </div>
      <!--  房产交易总套数-->
      <div class="right">
        <div class="title">
          房地产交易总值（元）
          <span
            :class="[
              { 'is-data-up': isBuildingUp },
              { 'is-data-down': !isBuildingUp }
            ]"
            style="margin-left: 0.5rem"
          >
            同比
            <span v-if="bulidingData.sameratio >= 0">↑</span>
            <span v-else>↓</span>
            {{ bulidingData.sameratio }}%
          </span>
        </div>
        <div class="building color">{{ bulidingData.yearprice }}</div>
      </div>
      <MapView />
    </div>
    <!-- 危房处置量 -->
    <div class="center-bottom grid-item">
      <!-- 标题 -->
      <div class="title">
        <span>危房处置量</span>
        <YearOrYearSwitch
          style="position: relative;top: -3.5rem;"
          :year="dangerousHouseIntervalCount"
        />
      </div>
      <div
        style="width: 400px;height:250px;left:1.54rem;top:4.31rem;font-size:0.92rem;position:absolute;"
      >
        <Chart :chartData="gcxmChart" />
      </div>
    </div>
    <!-- 行政审批 -->
    <div class="center-bottom grid-item center-bottom-right">
      <!-- 标题 -->
      <div class="title">
        <span>行政审批</span>
        <YearOrMonthSwitch class="yearOrMonth" :year="isThirdItemShowYear" />
      </div>
      <div style="margin-top:1rem;margin-left:1rem;width:100%;height:100%;">
        <!-- 上方三个数据展示框 -->
        <div
          style="display: flex;justify-content: center;width: 100%; margin-top: 2rem;margin-left: -1rem;"
        >
          <ShowRightThirdInfo
            title="总办件量"
            :number="auditData.total"
            unit1="件"
            style="border-right: 1px solid rgba(255,255,255,0.20);padding-right: 1.5rem;"
          />
          <ShowRightThirdInfo
            title="总平均用时"
            :number="auditData.avgtime"
            unit1="分钟/件"
            style="border-right: 1px solid rgba(255,255,255,0.20);padding-right: 1.5rem;"
          />
          <ShowRightThirdInfo
            title="总服务企业量"
            :number="auditData.totalservicecomp"
            unit1="家"
            style="margin-right:1rem"
          />
        </div>
        <!-- 左侧两个数据展示框 -->
        <div
          style="display: grid;float: left;border-right: 1px solid rgba(255,255,255,0.20);padding-right: 3rem;margin-top: 4rem;"
        >
          <ShowRightThirdInfo title="许可总办件量" :number="auditData.xktotal" unit1="件" />
          <ShowRightThirdInfo
            title="许可服务企业量"
            :number="auditData.xkservicecomp"
            unit1="件"
            style="margin-top: 4rem;"
          />
        </div>
        <CentSecondChart
          :chartData="socialHouseChartData.seriesData"
          style="float: left;padding-left: 2rem"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Chart from "../components/echart/center/GCXMChart";
import MapView from "../components/homePage/MapView";
// import MessageDiv from "../components/homePage/MessageDiv";
// import CenterFirstChart from "../components/echart/center/CenterFirstChart";
import CentSecondChart from "../components/echart/center/CentSecondChart";
import YearOrMonthSwitch from "../components/homePage/YearOrMonthSwitch";
import YearOrYearSwitch from "../components/homePage/YearOrYearSwitch";
import ShowRightThirdInfo from "../components/homePage/ShowRightThirdInfo";

export default {
  components: {
    Chart,
    MapView,
    // MessageDiv,
    // CenterFirstChart,
    CentSecondChart,
    YearOrMonthSwitch,
    ShowRightThirdInfo,
    YearOrYearSwitch
  },
  computed: {
    isBuildingUp: function() {
      if (this.bulidingData.sameratio > 0) {
        return true;
      } else {
        return false;
      }
    },
    isConstructionUp: function() {
      if (this.constructionData.cumulativetotalvalueyear > 0) {
        return true;
      } else {
        return false;
      }
    }
  },
  data() {
    return {
      // 危房处置量计时器执行次数
      dangerousHouseIntervalCount: 0,
      // 危房处置量
      gcxmChart: {
        data: {
          cszl: [1500, 1000, 2000],
          csczl: [1000, 800, 1500],
          nczl: [1000, 2000, 3000],
          ncczl: [800, 1700, 1500]
        },
        year2019: {
          cszl: [1500, 1000, 2000],
          csczl: [1000, 800, 1500],
          nczl: [1000, 2000, 3000],
          ncczl: [800, 1700, 1500]
        },
        year2018: {
          cszl: [1234, 1111, 2211],
          csczl: [1111, 1000, 2000],
          nczl: [1235, 2100, 2900],
          ncczl: [800, 1700, 1500]
        },
        year2017: {
          cszl: [800, 900, 1000],
          csczl: [700, 800, 900],
          nczl: [1000, 2000, 3000],
          ncczl: [9000, 1700, 2990]
        },
        year2016: {
          cszl: [1500, 1000, 2000],
          csczl: [1400, 200, 300],
          nczl: [522, 1236, 2222],
          ncczl: [300, 1000, 1111]
        }
      },
      // 控制行政审批是否按年显示
      isThirdItemShowYear: true,
      // 住房保障计时器的执行次数
      socialHouseIntervalCount: 1,
      // 保障房的高亮类
      // isShowSocialHouseHoverClass: true,
      // 房产交易展示数据是否为年 标识符
      isFirstItemShowYear: true,
      // 房产交易计时器执行次数
      houseTradeIntervalCount: 1,
      mapBuildingData: 0,
      bulidingData: {
        yearprice: 0.0,
        sameratio: 0,
        chainratio: 0
      },
      constructionData: {
        cumulativetotalvalueyear: 0,
        cumulativetotalvalue: 0
      },
      baseUrl: "http://10.10.208.6:30400/Statistics/",
      // 行政审批显示数据
      auditData: {
        data: {
          year: "2019",
          total: 0,
          avgtime: 0,
          totalservicecomp: 0,
          xktotal: 0,
          xkservicecomp: 0
        },
        // 存放当前年的住房保障数据
        year: {},
        // 存放当前月的住房保障数据
        month: {}
      },
      // 行政审批图标显示
      socialHouseChartData: {
        seriesData: {}
      },
      // 房产交易数据
      houseTradeData: {
        data: {
          total: "",
          totalareas: "",
          price: "",
          allprice: ""
        },
        // 单位
        unit: {
          total: "总套数(户)",
          allprice: "总成交价(亿元)",
          price: "平均价格(元)",
          totalareas: "总面积(㎡)"
        },
        year: {},
        month: {}
      },
      //
      houseTradeChartData: {
        xAxisData: ["12"],
        seriesData: {
          house: {
            name: "住宅",
            type: "line",
            stack: "总量",
            smooth: true,
            data: [1]
          },
          business: {
            name: "商业",
            type: "line",
            stack: "总量",
            smooth: true,
            data: [1]
          },
          office: {
            name: "办公",
            type: "line",
            stack: "总量",
            smooth: true,
            data: [2]
          },
          other: {
            name: "其他",
            type: "line",
            stack: "总量",
            smooth: true,
            data: [3]
          }
        }
      },
      // 房产交易按年的数据
      houseTradeYearData: [],
      // 房产交易按月的数据
      houseTradeMonthData: []
    };
  },
  mounted() {
    this.getDangerousHouse();
    // this.getSocialHouseData();
    this.getHouseTradeYear();
    this.getHouseTradeMonthArea();
    this.getThemeHouseTradeAll();
    this.getThemeConstruction();
    this.getThemeAuditYear(true);
    let _this = this;
    setInterval(function() {
      let tag = !_this.isThirdItemShowYear;
      if (tag) {
        _this.getThemeAuditYear(true);
      } else {
        _this.getThemeAuditYear(false);
      }
      _this.isThirdItemShowYear = tag;
    }, 10 * 1000);
  },

  methods: {
    getDangerousHouse() {
      // 开启定时，进行轮播
      let _this = this;
      setInterval(() => {
        let count = _this.dangerousHouseIntervalCount;
        count++;
        let mod = count % 4;
        // console.log(mod,count)
        switch (mod) {
          case 0: {
            _this.gcxmChart.data.cszl = _this.gcxmChart.year2019.cszl;
            _this.gcxmChart.data.cszcl = _this.gcxmChart.year2019.cszcl;
            _this.gcxmChart.data.nczl = _this.gcxmChart.year2019.nczl;
            _this.gcxmChart.data.nczcl = _this.gcxmChart.year2019.nczcl;
            break;
          }
          case 1: {
            _this.gcxmChart.data.cszl = _this.gcxmChart.year2018.cszl;
            _this.gcxmChart.data.cszcl = _this.gcxmChart.year2018.cszcl;
            _this.gcxmChart.data.nczl = _this.gcxmChart.year2018.nczl;
            _this.gcxmChart.data.nczcl = _this.gcxmChart.year2018.nczcl;
            break;
          }
          case 2: {
            _this.gcxmChart.data.cszl = _this.gcxmChart.year2017.cszl;
            _this.gcxmChart.data.cszcl = _this.gcxmChart.year2017.cszcl;
            _this.gcxmChart.data.nczl = _this.gcxmChart.year2017.nczl;
            _this.gcxmChart.data.nczcl = _this.gcxmChart.year2017.nczcl;
            break;
          }
          case 3: {
            _this.gcxmChart.data.cszl = _this.gcxmChart.year2016.cszl;
            _this.gcxmChart.data.cszcl = _this.gcxmChart.year2016.cszcl;
            _this.gcxmChart.data.nczl = _this.gcxmChart.year2016.nczl;
            _this.gcxmChart.data.nczcl = _this.gcxmChart.year2016.nczcl;
            break;
          }
        }
        _this.dangerousHouseIntervalCount = count;
      }, 5 * 1000);
    },
    // 获取行政审批数据
    getThemeAuditYear(isYear) {
      let url = {};
      let param = { year: 2019 };
      if (isYear) {
        url = this.baseUrl + "/GetThemeAuditYear";
      } else {
        url = this.baseUrl + "/GetThemeAuditMonth";
        param.month = 12;
      }
      this.http.post(url, param).then(response => {
        this.auditData.total = response.data[0].total;
        this.auditData.avgtime = response.data[0].avgtime;
        this.auditData.totalservicecomp = response.data[0].totalservicecomp;
        if (response.data[0].sorttotalname1 == "许可") {
          this.auditData.xktotal = response.data[0].sorttotal1;
        } else if (response.data[0].sorttotalname2 == "许可") {
          this.auditData.xktotal = response.data[0].sorttotal2;
        } else {
          this.auditData.xktotal = response.data[0].sorttotal3;
        }

        if (response.data[0].sortservicecompname1 == "许可") {
          this.auditData.xkservicecomp = response.data[0].sortservicecomp1;
        } else if (response.data[0].sortservicecompname2 == "许可") {
          this.auditData.xkservicecomp = response.data[0].sortservicecomp2;
        } else {
          this.auditData.xkservicecomp = response.data[0].sortservicecomp3;
        }

        // 计算当前的住房保障的图表数据
        this.socialHouseChartData.seriesData = {
          xktotal:
            (this.auditData.xktotal /
              (this.auditData.xktotal + this.auditData.xkservicecomp)) *
            100,
          xkservicecomp:
            (this.auditData.xkservicecomp /
              (this.auditData.xktotal + this.auditData.xkservicecomp)) *
            100
        };
      });
    },
    getSocialHouseData() {
      let url = this.baseUrl + "/GetThemeSocialHouse";
      this.http.post(url).then(response => {
        let resData = response.data[0];
        let socialHouseYear = {};
        let socialHouseMonth = {};
        //去掉年月，然后根据是否有cumulativee来区分年月数据
        Object.getOwnPropertyNames(resData).forEach(key => {
          if (key === "Year" || key === "Month") {
            console.log();
          } else if (!key.startsWith("Cumulativee")) {
            socialHouseMonth[key] = resData[key];
          } else {
            socialHouseYear[key.replace("Cumulativee", "")] = resData[key];
          }
        });
        // 将年月数据绑定到全局
        let auditData = {
          data: socialHouseYear,
          year: socialHouseYear,
          month: socialHouseMonth
        };
        this.auditData = auditData;
        // 计算当前的住房保障的图表数据
        this.socialHouseChartData.seriesData = this.calculateSocialHouseChartData(
          this.auditData.data
        );
        // 开启定时，进行轮播
        let _this = this;
        setInterval(() => {
          let count = _this.socialHouseIntervalCount;
          count++;
          let mod = count % 2;
          switch (mod) {
            case 0: {
              let data = _this.auditData.month;
              _this.auditData.data = data;
              // _this.isShowSocialHouseHoverClass = false;
              _this.isThirdItemShowYear = false;
              _this.socialHouseChartData.seriesData = _this.calculateSocialHouseChartData(
                data
              );
              break;
            }
            case 1: {
              let data = _this.auditData.year;
              _this.auditData.data = data;
              // _this.isShowSocialHouseHoverClass = true;
              _this.isThirdItemShowYear = true;
              _this.socialHouseChartData.seriesData = _this.calculateSocialHouseChartData(
                data
              );
              break;
            }
            // case 2: {
            //   let data = _this.auditData.year;
            //   _this.auditData.data = data;
            //   // _this.isShowSocialHouseHoverClass = false;
            //   _this.isThirdItemShowYear = true;
            //   _this.socialHouseChartData.seriesData = _this.calculateSocialHouseChartData(
            //     data,
            //     true
            //   );
            //   break;
            // }
            // case 3: {
            //   let data = _this.auditData.month;
            //   _this.auditData.data = data;
            //   // _this.isShowSocialHouseHoverClass = true;
            //   _this.isThirdItemShowYear = false;
            //   _this.socialHouseChartData.seriesData = _this.calculateSocialHouseChartData(
            //     data,
            //     false
            //   );
            //   break;
            // }
          }
          _this.socialHouseIntervalCount = count;
        }, 10 * 1000);
      });
    },
    // 根据住房保障的数据计算图表需要的显示数据 data为当月或当年的显示数据 isArea为true时获取面积占比的数据，反之，获取数量占比数据
    calculateSocialHouseChartData(data) {
      if (!data) {
        return;
      }

      // let ShantyTownNewWork,
      //     SubsidizedHousingPrjCompleted,
      //     PublicHouseRentalSubsidy,
      //     PublicHouseAssigned = "";
      // if (isArea) {
      //   // total = "totalareas";
      //   newsocialhouse = "newsocialhouseareas";
      //   publichouse = "publichouseareas";
      //   affordablehouse = "affordablehouseareas";
      //   lowrenthouse = "lowrenthouseareas";
      // } else {
      //   total = "total";
      //   newsocialhouse = "newsocialhousenum";
      //   publichouse = "publichousenum";
      //   affordablehouse = "affordablehousenum";
      //   lowrenthouse = "lowrenthousenum";
      // }
      let seriesData = {
        //棚户区改造新开工
        ShantyTownNewWorkRatio:
          // [
          //   { name: "another", value: data["ShantyTownNewWork"] },
          //   { name: "another1", value: data["ShantyTownNewWork"] }
          // ]
          data["ShantyTownNewWorkRatio"],
        //保障安居工程竣工
        SubsidizedHousingPrjCompletedRatio:
          // [
          //   { name: "another", value: data[total] - data[publichouse] },
          //   { name: "another2", value: data[publichouse] }
          // ]
          data["SubsidizedHousingPrjCompletedRatio"],
        //公租房租赁补贴
        PublicHouseRentalSubsidyRatio:
          // [
          //   { name: "another", value: data[total] - data[affordablehouse] },
          //   { name: "another3", value: data[affordablehouse] }
          // ]
          data["PublicHouseRentalSubsidyRatio"],
        //公共租赁住房分配
        PublicHouseAssignedRatio:
          // [
          //   { name: "another", value: data[total] - data[lowrenthouse] },
          //   { name: "another4", value: data[lowrenthouse] }
          // ]
          data["PublicHouseAssignedRatio"]
      };
      return seriesData;
    },
    // 获取按年的房产交易数据
    getHouseTradeYear() {
      let url = this.baseUrl + "/GetThemeHouseTradeYear";
      this.http.post(url, { year: 2019 }).then(response => {
        let resData = response.data;
        let houseTradeData = {};
        houseTradeData.total = resData.yeartotal;
        houseTradeData.totalareas = parseInt(resData.yeartotalareas);
        houseTradeData.allprice = (resData.yearprice / 100000000).toFixed(3);
        houseTradeData.price = parseInt(resData.yearavgprice);
        this.houseTradeData.year = houseTradeData;
        this.houseTradeData.data = houseTradeData;
        let model = resData.model;
        this.houseTradeYearData = model;

        this.changeHouseTradeCharts(model, "num", true, this);

        let _this = this;
        setInterval(function() {
          let count = _this.houseTradeIntervalCount;
          count++;
          let mod = count % 8;
          _this.houseTradeIntervalCount = count;
          switch (mod) {
            case 1: {
              _this.isFirstItemShowYear = true;
              _this.houseTradeData.data = _this.houseTradeData.year;
              _this.changeHouseTradeCharts(
                _this.houseTradeYearData,
                "num",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
            case 2: {
              _this.isFirstItemShowYear = true;
              _this.houseTradeData.data = _this.houseTradeData.year;
              _this.changeHouseTradeCharts(
                _this.houseTradeYearData,
                "areas",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
            case 3: {
              _this.isFirstItemShowYear = true;
              _this.houseTradeData.data = _this.houseTradeData.year;
              _this.changeHouseTradeCharts(
                _this.houseTradeYearData,
                "avgprice",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
            case 4: {
              _this.isFirstItemShowYear = true;
              _this.changeHouseTradeCharts(
                _this.houseTradeYearData,
                "price",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
            case 5: {
              _this.isFirstItemShowYear = false;
              _this.houseTradeData.data = _this.houseTradeData.month;
              _this.changeHouseTradeCharts(
                _this.houseTradeMonthData,
                "num",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
            case 6: {
              _this.isFirstItemShowYear = false;
              _this.houseTradeData.data = _this.houseTradeData.month;
              _this.changeHouseTradeCharts(
                _this.houseTradeMonthData,
                "areas",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
            case 7: {
              _this.isFirstItemShowYear = false;
              _this.houseTradeData.data = _this.houseTradeData.month;
              _this.changeHouseTradeCharts(
                _this.houseTradeMonthData,
                "avgprice",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
            case 0: {
              _this.isFirstItemShowYear = false;
              _this.houseTradeData.data = _this.houseTradeData.month;
              _this.changeHouseTradeCharts(
                _this.houseTradeMonthData,
                "price",
                _this.isFirstItemShowYear,
                _this
              );
              break;
            }
          }
        }, 5 * 1000);
      });
    },
    // 获取按月的房产交易数据
    getHouseTradeMonthArea() {
      let url = this.baseUrl + "/GetThemeHouseTradeMonthArea";
      this.http.post(url, { year: 2019, month: 12 }).then(response => {
        let resData = response.data;
        let houseTradeData = {};
        houseTradeData.total = resData.monthtotal;
        houseTradeData.totalareas = parseInt(resData.monthtotalareas);
        houseTradeData.allprice = (resData.monthprice / 100000000).toFixed(3);
        houseTradeData.price = parseInt(resData.monthavgprice);
        this.houseTradeData.month = houseTradeData;
        let model = resData.model;
        this.houseTradeMonthData = model;
        // let result = this.changeHouseTradeCharts(model, 'num', false)
      });
    },
    changeHouseTradeCharts(data, type, isYear, _this) {
      let seriesData = {};
      let tagArr = ["house", "business", "office", "other"];
      let newTagArr = []; //存放需要的字段名称
      // 根据type生产需要的字段名称
      for (let i = 0; i < tagArr.length; i++) {
        let tag = "";
        if (type === "avgprice") {
          tag = "avg" + tagArr[i] + "price";
        } else {
          tag = tagArr[i] + type;
        }
        newTagArr.push(tag);
        seriesData[tagArr[i]] = [];
      }
      let xAxisData = [];
      data.forEach(item => {
        if (isYear) {
          xAxisData.unshift(item.month);
        } else {
          xAxisData.push(item.areaname);
        }

        for (let i = 0; i < 4; i++) {
          if (isYear) {
            seriesData[tagArr[i]].unshift(item[newTagArr[i]]);
            // xAxisData.shift(item.month);
          } else {
            seriesData[tagArr[i]].push(item[newTagArr[i]]);
            // xAxisData.push(item.areaname);
          }
        }
      });
      _this.houseTradeChartData.xAxisData = xAxisData;
      tagArr.forEach(item => {
        _this.houseTradeChartData.seriesData[item].data = seriesData[item];
      });
    },
    // 根据计时器切换房产交易右侧的按钮的选中状态
    selectedMessageDivByTime(data) {
      let count = this.houseTradeIntervalCount;
      let mod = count % 4;
      if (mod === data) {
        return true;
      } else {
        return false;
      }
    },
    // 显示大屏数字变化过程 value为变化后的数字 tag为字段名称 item子字段名称 详细参考this.bulidingData字段
    oldValueToNewValue(value, tag, item) {
      let isAdd = true;
      let newValue = value;
      // 获取要变化的data数据
      let oldValue = this[tag][item];
      if (newValue > oldValue) {
        isAdd = true;
      } else if (newValue < oldValue) {
        isAdd = false;
      } else {
        return;
      }
      let _this = this;
      let i = 0;
      // 开启定时变化
      let timeId = setInterval(function() {
        let data = _this[tag][item];
        i++;
        if (isAdd) {
          data += Math.pow(2, i);
          if (data >= value) {
            _this[tag][item] = value;
            clearInterval(timeId);
          } else {
            _this[tag][item] = data;
          }
        } else {
          data -= Math.pow(2, i);
          if (data <= value) {
            _this[tag][item] = value;
            clearInterval(timeId);
          } else {
            _this[tag][item] = data;
          }
        }
      }, 100);
    },
    // 获取大屏数据房产交易
    getThemeHouseTradeAll() {
      let url = this.baseUrl + "/GetThemeHouseTradeAll";
      this.http.post(url, { year: 2019, month: 12 }).then(response => {
        let resData = response.data;
        this.bulidingData.sameratio = resData.sameratio;
        this.oldValueToNewValue(
          parseInt(response.data.yearprice),
          "bulidingData",
          "yearprice"
        );
      });
    },
    // 获取大屏数据建筑业产值
    getThemeConstruction() {
      let url = this.baseUrl + "/GetThemeConstruction";
      this.http.post(url, { year: 2019, month: 11 }).then(response => {
        this.constructionData.cumulativetotalvalueyear =
          response.data[0].cumulativetotalvalueyear;
        this.oldValueToNewValue(
          response.data[0].cumulativetotalvalue * 100000000,
          "constructionData",
          "cumulativetotalvalue"
        );
      });
    }
  }
};
</script>

<style lang="scss">
@import "../assets/scss/center.scss";

.year_zps_ul {
  display: flex;
  position: absolute;
  left: 20.46rem;
  top: 0rem;
  li {
    border: 1px solid #1856fd;
    width: 3.07rem;
    height: 1.85rem;
    font-size: 0.92rem;
    line-height: 1.85rem;
    text-align: center;
    &.active {
      background: #1856fd;
    }
  }
}
</style>
