<template>
  <div id="right" class="multiple-item-bg">
    <!-- 重大项目 -->
    <div>
      <!-- 房地产市场 -->
      <div class="house">
        房地产市场
        <div class="first">
          <span class="text">总成交金额</span>
          <span class="text1">千万(元)</span>
          <span class="text2">
            <countTo :separator="a" :endVal="fdc_zcjje"></countTo>
          </span>
          <img src="../assets/right/fang.png" alt style="width:15.38rem;height:4.31rem" />
        </div>
        <div class="first1">
          <span class="text">总套数</span>
          <span class="text1">(套)</span>
          <span class="text2">
            <countTo :separator="a" :endVal="fdc_zts"></countTo>
          </span>
          <img src="../assets/right/fang.png" alt style="width:15.38rem;height:4.31rem" />
        </div>
        <div class="first2">
          <span class="text">总面积</span>
          <span class="text1">(m²)</span>
          <span class="text2">
            <countTo :separator="a" :endVal="fdc_zmj"></countTo>
          </span>
          <img src="../assets/right/fang.png" alt style="width:15.38rem;height:4.31rem" />
        </div>
        <div class="first3">
          <span class="text">库存量</span>
          <span class="text1">(套)</span>
          <span class="text2">
            <countTo :separator="a" :endVal="fdc_kcl"></countTo>
          </span>
          <img src="../assets/right/fang.png" alt style="width:15.38rem;height:4.31rem" />
        </div>
        <div id="main" style="
    left: 0px;
    top: 17px;
    width: 556px;
    height: 393px;">
          <!-- <div id="main" style="width: 400px;height:400px;"></div> -->
          <Fangzi :chartData="aaaa"></Fangzi>
        </div>
      </div>

      <div class="grid-item">
        <div class="title">
          <span>{{greatProjectData.prjName}}项目进度情况</span>
        </div>
        <div style="margin-top: 2rem;margin-left: 0.5rem;">
          <RightFirstProgress :data="greatProjectData.mainList.ratio" />
        </div>
        <div class="right-first-circle">
          <div class="right-first-target-circle bg_circle Rotation"></div>
          <div class="right-first-target-circle">
            <div>
              <div class="circle-data">{{greatProjectData.otherList.ratio * 100}}%</div>
              <div class="circle-title">{{greatProjectData.otherList.Name}}</div>
            </div>
          </div>
          <RightFirstInfo
            :imgurl="imgUrl.one"
            :title="greatProjectData.otherList.SubQuota[0].Name"
            :data="greatProjectData.otherList.SubQuota[0].ratio"
            v-if="isShowRightFirstInfo(1)"
            class="first"
          />
          <RightFirstInfo
            :imgurl="imgUrl.two"
            :title="greatProjectData.otherList.SubQuota[1].Name"
            :data="greatProjectData.otherList.SubQuota[1].ratio"
            v-if="isShowRightFirstInfo(2)"
            class="second"
          />
          <RightFirstInfo
            :imgurl="imgUrl.three"
            :title="greatProjectData.otherList.SubQuota[2].Name"
            :data="greatProjectData.otherList.SubQuota[2].ratio"
            v-if="isShowRightFirstInfo(3)"
            class="third"
          />
          <RightFirstInfo
            :imgurl="imgUrl.four"
            :title="greatProjectData.otherList.SubQuota[3].Name"
            :data="greatProjectData.otherList.SubQuota[3].ratio"
            v-if="isShowRightFirstInfo(4)"
            class="four"
          />
        </div>
      </div>
    </div>
    <!-- 行政审批 -->
  </div>
</template>

<script>
import countTo from "vue-count-to";
import Fangzi from "../components/echart/right/fangzi";
import RightFirstProgress from "../components/homePage/RightFirstProgress";
import RightFirstInfo from "../components/homePage/RightFirstInfo";
export default {
  components: {
    countTo,
    Fangzi,
    RightFirstProgress,
    RightFirstInfo
  },
  data() {
    return {
      a: "1",
      // 总成交金额
      fdc_zcjje: 0,
      // 总面积
      fdc_zmj: 0,
      // 总套数
      fdc_zts: 0,
      // 库存量
      fdc_kcl: 0,
      // 商品房成交量
      fdc_zzcjl_spf: 0,
      aaaa: {
        aa: [63, 58, 68, 62, 58, 60, 62, 60, 65, 58, 60, 62, 60]
      },
      // 控制行政审批是否按年显示
      isThirdItemShowYear: true,
      // imgUrl: require("../assets/right/first/earth.png"),
      imgUrl: {
        one: require("../assets/right/first/point.png"),
        two: require("../assets/right/first/earth.png"),
        three: require("../assets/right/first/fire.png"),
        four: require("../assets/right/first/building.png")
      },
      baseUrl: "http://10.10.208.6:30400/Statistics",
      // 危房数据显示
      dangerousHouseData: {
        xAxisData: ["1"],
        seriesData: {
          citynums: [1],
          citydealnums: [2],
          villagenums: [3],
          villagedealnums: [4]
        }
      },
      // 行政审批显示数据
      auditData: {
        year: "2019",
        total: 2000,
        avgtime: 24.5,
        totalservicecomp: 4000,
        sorttotal1: 1,
        sorttotalname1: "1",
        sorttotal2: 1,
        sorttotalname2: "1",
        sorttotal3: 1,
        sorttotalname3: "1",
        sortservicecomp1: 1,
        sortservicecompname1: "1",
        sortservicecomp2: 1,
        sortservicecompname2: "1",
        sortservicecomp3: 1,
        sortservicecompname3: "1"
      },
      // 重大项目显示数据
      greatProjectData: {
        prjName: "污水处理设施清洁排放技术改造",
        mainList: {
          Name: "总投资（万元）",
          ratio: 0.67
        },
        otherList: {
          Name: "总投资（万元）",
          PlanValue: 50000,
          RealValue: 33400,
          ratio: 0.67,
          SubQuota: [
            {
              Name: "总投资（万元）",
              PlanValue: 12500,
              RealValue: 8800,
              ratio: 0.7,
              SubQuota: []
            },
            {
              Name: "总投资（万元）",
              PlanValue: 12500,
              RealValue: 8000,
              ratio: 0.64,
              SubQuota: []
            },
            {
              Name: "总投资（万元）",
              PlanValue: 12500,
              RealValue: 8100,
              ratio: 0.65,
              SubQuota: []
            },
            {
              Name: "总投资（万元）",
              PlanValue: 12500,
              RealValue: 8500,
              ratio: 0.68,
              SubQuota: []
            }
          ]
        }
      },
      // 保存重大项目接口获取的数据
      getGreatProjectDatas: {},
      //控制行政审批的柱状图形的高度
      colorDivCss: {
        blue: 15,
        red: 15,
        yellow: 15,
        green: 15
      }
    };
  },
  mounted() {
    let param = { path: "ov", groupid: 20 };
    this.http({
      url: "http://10.10.208.6:2020/home/serv",
      params: param,
      methods: "post"
    }).then(res => {
      // console.log(res.data);
      this.fdc_zcjje = Math.ceil(res.data.fdc_zcjje / 1000);
      this.fdc_zmj = Number(res.data.fdc_zmj.toFixed(0));
      this.fdc_zts = res.data.fdc_zts;
      this.fdc_kcl = res.data.fdc_kcl;
    });
    let param1 = { path: "ov", groupid: 21 };
    this.http({
      url: "http://10.10.208.6:2020/home/serv",
      params: param1,
      methods: "post"
    }).then(res => {
      console.log(res.data.fdc_zzcjl_spf);
    });
    this.getDangerousHouse();
    this.getThemeAuditYear(true);
    this.getGreatProject();
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
    // 获取危房数据
    getDangerousHouse() {
      let url = this.baseUrl + "/GetThemeDangerousHouse";
      this.http.post(url).then(response => {
        let resData = response.data;
        let xAxisData = [];
        let citynums = [];
        let citystartworknum = [];
        let cityendworknum = [];
        let villagenums = [];
        let villagestartworknum = [];
        let villageendworknum = [];
        resData.forEach(item => {
          citynums.push(item.citynum);
          citystartworknum.push(item.citystartworknum);
          cityendworknum.push(item.cityendworknum);
          villagenums.push(item.villagenum);
          villagestartworknum.push(item.villagestartworknum);
          xAxisData.push(item.areaname);
          villageendworknum.push(item.villageendworknum);
        });
        let dangerousHouseData = [];
        dangerousHouseData.xAxisData = xAxisData;
        dangerousHouseData.seriesData = {};
        dangerousHouseData.seriesData.citynums = citynums;
        dangerousHouseData.seriesData.citystartworknum = citystartworknum;
        dangerousHouseData.seriesData.cityendworknum = cityendworknum;
        dangerousHouseData.seriesData.villagenums = villagenums;
        dangerousHouseData.seriesData.villagestartworknum = villagestartworknum;
        dangerousHouseData.seriesData.villageendworknum = villageendworknum;
        this.dangerousHouseData = dangerousHouseData;
      });
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
        let resData = response.data[0];
        this.auditData = resData;
        // this.$refs.greendiv.style= 'height:'
        if (resData.sorttotal1 > resData.sorttotal2) {
          this.colorDivCss.green =
            (15 * resData.sorttotal2) / resData.sorttotal1;
        } else {
          this.colorDivCss.blue =
            (15 * resData.sorttotal1) / resData.sorttotal2;
        }
        if (resData.sortservicecomp1 > resData.sortservicecomp2) {
          this.colorDivCss.red =
            (15 * resData.sortservicecomp2) / resData.sortservicecomp1;
        } else {
          this.colorDivCss.yellow =
            (15 * resData.sortservicecomp1) / resData.sortservicecomp2;
        }
      });
    },
    // 获取重大项目数据
    getGreatProject() {
      let url = this.baseUrl + "/GetThemeGreatProject";
      this.http.post(url).then(response => {
        this.getGreatProjectDatas = response.data;
        let res = {
          prjName: this.getGreatProjectDatas.prjName,
          mainList: this.getGreatProjectDatas.mainList[0],
          otherList: this.getGreatProjectDatas.otherList[0]
        };
        this.greatProjectData = res;

        let _this = this;
        let count = 0;
        setInterval(function() {
          count++;
          let otherLists = _this.getGreatProjectDatas.otherList;
          let length = otherLists.length;
          let otherList = otherLists[count % length];
          _this.greatProjectData.otherList = otherList;
        }, 5 * 1000);
      });
    },
    // 控制第一个重大子项目是否显示
    isShowRightFirstInfo(value) {
      let subQuota = this.greatProjectData.otherList.SubQuota;
      if (subQuota.length < value) {
        return false;
      } else {
        return true;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/right.scss";
</style>
