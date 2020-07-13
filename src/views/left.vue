<template>
  <div id="left" class="multiple-item-bg">
    <!-- 建筑业统计 -->
    <div class="grid-item">
      <!-- 标题 -->
      <div class="title">
        <span>建筑业统计</span>
        <YearOrMonthSwitch class="yearOrMonth" :year="isFirstItemShowYear" />
      </div>
      <div style class="first-charts-root">
        <!-- 建筑图片 -->
        <img
          src="../assets/left/building.png"
          style="position: relative;width: 16.125rem;height: 19.3125rem;left: 9rem;top: 7rem;"
        />
        <transition name="play-one-animation" :after-leave="afterLeave">
          <ShowLeftFirstInfo
            unit="㎡"
            ref="one"
            :data="this.StatisticsOfConstructionData.data.energysavingareas"
            title="公众建筑节能改造"
            :periodofyear="this.StatisticsOfConstructionData.data.energysavingoveryear"
            :class="['one','heart']"
            v-if="isPlayBuildingFirstItem"
          />
        </transition>

        <ShowLeftFirstInfo
          unit="㎡"
          ref="two"
          :data="this.StatisticsOfConstructionData.data.industrializeareas"
          title="建筑工业化面积"
          :periodofyear="this.StatisticsOfConstructionData.data.industrializeoveryear"
          class="two heart"
        />
        <ShowLeftFirstInfo
          unit="㎡"
          :data="this.StatisticsOfConstructionData.data.houseconstructionareas"
          title="房屋施工面积"
          :periodofyear="this.StatisticsOfConstructionData.data.houseconstructionoveryear"
          class="third heart"
        />
        <ShowLeftFirstInfo
          unit="㎡"
          :data="this.StatisticsOfConstructionData.data.newconstrructionareas"
          title="新开工面积"
          :periodofyear="this.StatisticsOfConstructionData.data.newconstrructionoveryear"
          class="four heart"
          style="white-space:nowrap;margin-left: 0.9rem;"
        />
      </div>
    </div>
    <!-- 园林市政 -->
    <div class="grid-item">
      <div class="title">
        <span>园林市政</span>
      </div>
      <div style="height: 1rem;">
        <!-- 污水处理能力 -->
        <div style="position: relative;left: 1.53rem;top: 5.85rem;">
          <img src="../assets/left/total_enterprises.png" style="width: 15.62rem;height: 9.54rem;" />
          <span class="border-title">污水处理能力</span>
          <span class="border-number building color">{{ylsz_szjs_xzwsclnl}}</span>
          <span class="border-unit">座</span>
          <span
            class="border-tb"
            :style="ylsz_szjs_xzwsclnl_bfb >= 0 ? 'color: #FF4965;' : 'color: #44C787;'"
          >
            同比
            <span
              style="padding-left: 1rem;float: right;"
              v-if="ylsz_szjs_xzwsclnl_bfb >= 0"
            >↑ {{ylsz_szjs_xzwsclnl_bfb}}%</span>
            <span style="padding-left: 1rem;float: right;" v-else>↓ {{-ylsz_szjs_xzwsclnl_bfb}}%</span>
          </span>
        </div>
        <!-- 新建雨水管网 -->
        <div style="position: relative;left: 18.6rem;top: -4rem;">
          <img src="../assets/left/total_enterprises.png" style="width: 15.62rem;height: 9.54rem;" />
          <span class="border-title">新建雨水管网</span>
          <span class="border-number building color">{{ylsz_szjs_xzysgw}}</span>
          <span class="border-unit">km</span>
          <span
            class="border-tb"
            :style="ylsz_szjs_xzysgw_bfb >= 0 ? 'color: #FF4965;' : 'color: #44C787;'"
          >
            同比
            <span
              style="padding-left: 1rem;float: right;"
              v-if="ylsz_szjs_xzysgw_bfb >= 0"
            >↑ {{ylsz_szjs_xzysgw_bfb}}%</span>
            <span style="padding-left: 1rem;float: right;" v-else>↓ {{-ylsz_szjs_xzysgw_bfb}}%</span>
          </span>
        </div>
        <!-- 新增应急设备 -->
        <div style="position: relative;left: 1.53rem;top: -1.5rem;">
          <img src="../assets/left/total_enterprises.png" style="width: 15.62rem;height: 9.54rem;" />
          <span class="border-title">新增应急设备</span>
          <span class="border-number building color">{{ylsz_szjs_xzyjsb}}</span>
          <span class="border-unit">个</span>
          <span
            class="border-tb"
            :style="ylsz_szjs_xzyjsb_bfb >= 0 ? 'color: #FF4965;' : 'color: #44C787;'"
          >
            同比
            <span
              style="padding-left: 1rem;float: right;"
              v-if="ylsz_szjs_xzyjsb_bfb >= 0"
            >↑ {{ylsz_szjs_xzyjsb_bfb}}%</span>
            <span style="padding-left: 1rem;float: right;" v-else>↓ {{-ylsz_szjs_xzyjsb_bfb}}%</span>
          </span>
        </div>
        <!-- 雨污分流改造管网 -->
        <div style="position: relative;left: 18.6rem;top: -11.5rem;">
          <img src="../assets/left/total_enterprises.png" style="width: 15.62rem;height: 9.54rem;" />
          <span class="border-title" style="letter-spacing: -1px;">雨污分流改造管网</span>
          <span class="border-number building color">{{ylsz_szjs_ywflgzgw}}</span>
          <span class="border-unit">km</span>
          <span
            class="border-tb"
            :style="ylsz_szjs_ywflgzgw_bfb >= 0 ? 'color: #FF4965;' : 'color: #44C787;'"
          >
            同比
            <span
              style="padding-left: 1rem;float: right;"
              v-if="ylsz_szjs_ywflgzgw_bfb >= 0"
            >↑ {{ylsz_szjs_ywflgzgw_bfb}}%</span>
            <span style="padding-left: 1rem;float: right;" v-else>↓ {{-ylsz_szjs_ywflgzgw_bfb}}%</span>
          </span>
        </div>
        <!-- 新增停车位 -->
        <div style="position: relative;left: 1.53rem;top: -8.5rem;">
          <img src="../assets/left/total_enterprises.png" style="width: 15.62rem;height: 9.54rem;" />
          <span class="border-title">新增停车位</span>
          <span class="border-number building color">{{ylsz_szjs_xztcw}}</span>
          <span class="border-unit">个</span>
          <span
            class="border-tb"
            :style="ylsz_szjs_xztcw_bfb >= 0 ? 'color: #FF4965;' : 'color: #44C787;'"
          >
            同比
            <span
              style="padding-left: 1rem;float: right;"
              v-if="ylsz_szjs_xztcw_bfb >= 0"
            >↑ {{ylsz_szjs_xztcw_bfb}}%</span>
            <span style="padding-left: 1rem;float: right;" v-else>↓ {{-ylsz_szjs_xztcw_bfb}}%</span>
          </span>
        </div>
        <!-- 道路改造建设 -->
        <div style="position: relative;left: 18.6rem;top: -18.3rem;">
          <img src="../assets/left/total_enterprises.png" style="width: 15.62rem;height: 9.54rem;" />
          <span class="border-title">道路改造建设</span>
          <span class="border-number building color">{{ylsz_szjs_dlgzjs}}</span>
          <span class="border-unit">km</span>
          <span
            class="border-tb"
            :style="ylsz_szjs_dlgzjs_bfb >= 0 ? 'color: #FF4965;' : 'color: #44C787;'"
          >
            同比
            <span
              style="padding-left: 1rem;float: right;"
              v-if="ylsz_szjs_dlgzjs_bfb >= 0"
            >↑ {{ylsz_szjs_dlgzjs_bfb}}%</span>
            <span style="padding-left: 1rem;float: right;" v-else>↓ {{-ylsz_szjs_dlgzjs_bfb}}%</span>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ShowLeftFirstInfo from "../components/homePage/ShowLeftFirstInfo";
import YearOrMonthSwitch from "../components/homePage/YearOrMonthSwitch";
export default {
  components: {
    ShowLeftFirstInfo,
    YearOrMonthSwitch
  },
  data() {
    return {
      count: 1,
      isFirstItemShowYear: true,
      isPlayBuildingFirstItem: true,
      theBaseUrl: "http://10.10.208.6:30400/Statistics",
      StatisticsOfConstructionData: {
        data: {
          energysavingareas: 0,
          industrializeareas: 0,
          houseconstructionareas: 0,
          newconstrructionareas: 0,
          energysavingoveryear: 0,
          industrializeoveryear: 0,
          houseconstructionoveryear: 0,
          newconstrructionoveryear: 0
        }
      },
      // 新增污水处理能力(座)
      ylsz_szjs_xzwsclnl: 0,
      // 新增污水处理能力百分比(%)
      ylsz_szjs_xzwsclnl_bfb: 0,
      // 新增雨水管网(km)
      ylsz_szjs_xzysgw: 0,
      // 新增雨水管网百分比(%)
      ylsz_szjs_xzysgw_bfb: 0,
      // 新增应急设备(个)
      ylsz_szjs_xzyjsb: 0,
      // 新增应急设备百分比(%)
      ylsz_szjs_xzyjsb_bfb: 0,
      // 雨污分流改造管网(km)
      ylsz_szjs_ywflgzgw: 0,
      // 雨污分流改造管网百分比(%)
      ylsz_szjs_ywflgzgw_bfb: 0,
      // 新增停车位
      ylsz_szjs_xztcw: 0,
      // 新增停车位同比
      ylsz_szjs_xztcw_bfb: 0,
      // 道路改造建设
      ylsz_szjs_dlgzjs: 0,
      // 道路改造建设同比
      ylsz_szjs_dlgzjs_bfb: 0
    };
  },
  mounted() {
    this.getStatisticsOfConstruction();
    this.getYlsz();
  },
  methods: {
    afterLeave() {
      this.isPlayBuildingFirstItem = true;
    },
    // 建筑业统计接口
    getStatisticsOfConstruction() {
      let url = this.theBaseUrl + "/GetThemeConstruction";
      this.http.post(url).then(response => {
        this.StatisticsOfConstructionData = response.data[0];
        let resData = response.data[0];
        let year = {};
        let month = {};
        Object.getOwnPropertyNames(resData).forEach(key => {
          if (key === "year" || key === "month") {
            // console.log();
          } else {
            let value = resData[key];
            if (key.startsWith("cumulative")) {
              year[key.replace("cumulative", "")] = value;
            } else {
              month[key] = value;
            }
          }
        });
        let StatisticsOfConstructionData = this.StatisticsOfConstructionData;
        StatisticsOfConstructionData.data = year;
        StatisticsOfConstructionData.year = year;
        StatisticsOfConstructionData.month = month;
        let _this = this;
        setInterval(function() {
          _this.isFirstItemShowYear = !_this.isFirstItemShowYear;
          _this.isPlayBuildingFirstItem = !_this.isPlayBuildingFirstItem;
          _this.isPlayBuildingFirstItem = !_this.isPlayBuildingFirstItem;
          if (_this.isFirstItemShowYear) {
            _this.StatisticsOfConstructionData.data =
              _this.StatisticsOfConstructionData.year;
          } else {
            _this.StatisticsOfConstructionData.data =
              _this.StatisticsOfConstructionData.month;
          }
        }, 10 * 1000);
      });
    },

    // 园林市政接口
    getYlsz() {
      let vm = this;
      let url = "http://10.10.208.6:2020/home/serv";
      let param = { path: "ov", groupid: 13 };
      vm.http({ url: url, method: "post", params: param }).then(res => {
        vm.oldValueToNewValue(
          Math.round(res.data.ylsz_szjs_xzwsclnl),
          "ylsz_szjs_xzwsclnl"
        );
        vm.ylsz_szjs_xzwsclnl_bfb = res.data.ylsz_szjs_xzwsclnl_bfb;
        vm.oldValueToNewValue(
          Math.round(res.data.ylsz_szjs_xzysgw),
          "ylsz_szjs_xzysgw"
        );
        vm.ylsz_szjs_xzysgw_bfb = res.data.ylsz_szjs_xzysgw_bfb;
        vm.oldValueToNewValue(
          Math.round(res.data.ylsz_szjs_xzyjsb),
          "ylsz_szjs_xzyjsb"
        );
        vm.ylsz_szjs_xzyjsb_bfb = res.data.ylsz_szjs_xzyjsb_bfb;
        vm.oldValueToNewValue(
          Math.round(res.data.ylsz_szjs_ywflgzgw),
          "ylsz_szjs_ywflgzgw"
        );
        vm.ylsz_szjs_ywflgzgw_bfb = res.data.ylsz_szjs_ywflgzgw_bfb;
        vm.oldValueToNewValue(
          Math.round(res.data.ylsz_szjs_xztcw),
          "ylsz_szjs_xztcw"
        );
        vm.ylsz_szjs_xztcw_bfb = res.data.ylsz_szjs_xztcw_bfb;
        vm.oldValueToNewValue(
          Math.round(res.data.ylsz_szjs_dlgzjs),
          "ylsz_szjs_dlgzjs"
        );
        vm.ylsz_szjs_dlgzjs_bfb = res.data.ylsz_szjs_dlgzjs_bfb;
      });
    },
    // 显示大屏数字变化过程 value为变化后的数字 tag为字段名称
    oldValueToNewValue(value, tag) {
      let isAdd = true;
      let newValue = value;
      // 获取要变化的data数据
      let oldValue = this[tag];
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
        let data = _this[tag];
        i++;
        if (isAdd) {
          data += Math.pow(2, i);
          if (data >= value) {
            _this[tag] = value;
            clearInterval(timeId);
          } else {
            _this[tag] = data;
          }
        } else {
          data -= Math.pow(2, i);
          if (data <= value) {
            _this[tag] = value;
            clearInterval(timeId);
          } else {
            _this[tag] = data;
          }
        }
      }, 100);
    }
  }
};
</script>

<style lang="scss" >
@import "../assets/scss/left.scss";
</style>
