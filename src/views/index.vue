<template>
  <div id="index">
    <dv-full-screen-container class="bg">
      <dv-loading v-show="loading">Loading...</dv-loading>
      <!-- 标题行 -->
      <div v-show="!loading" class="host-body">
        <div class="title">
          <div class="head-left">
            <div>
              <span class="font" style="margin-left:0">城市建设</span>
              <span class="font">房地产数据展示</span>
              <span class="font">园林市政</span>
            </div>
          </div>
          <div class="head-right">
            <div>
              <span class="font" style="margin-left:0">农村生活污水</span>
              <span class="font">危房排查及改造</span>
              <span class="font">历史文化建设</span>
            </div>
          </div>
          <span class="head-title-font">城建行业综合监测平台</span>
        </div>
      </div>
      <!-- 内容主要部分 -->
      <div v-show="!loading" id="indexBody">
        <!-- 左边三个 -->

        <left />

        <!-- 中间部分 -->

        <center />

        <!-- 右边三个 -->

        <right />
      </div>
    </dv-full-screen-container>
  </div>
</template>

<script>
import left from "./left";
import right from "./right";
import center from "./center1";
export default {
  data() {
    return {
      loading: true
    };
  },
  components: {
    left,
    center,
    right
  },
  mounted() {
    this.cancelLoading();
  },
  methods: {
    cancelLoading() {
      // this.loading = false;
      setTimeout(() => {
       this.loading = false;
      }, 2500);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "../assets/scss/index.scss";
#indexBody {
  // display: grid;
  // grid-template-columns: 25% 50% 25%;
  // grid-column-gap: 1rem;
  // width: 99%;
  // height: 94%;
  // padding: 1rem;
  display: grid;
  grid-template-columns: 25% 50% 25%;
  width: 100%;
  height: 94%;
  padding: 14px;
}
.item {
  font-size: 2em;
  text-align: center;
  border: 1px solid #e5e4e9;
}
.left-first {
  background-color: #222222;
  grid-row-start: 1;
  grid-row-end: 4;
}
.center-top {
  background-color: #ef342a;
  grid-column-start: 2;
  grid-column-end: 4;
  grid-row-start: 1;
  grid-row-end: 3;
}
</style>
