<template>
  <div class="right-first-root">
    <div style="margin-left: 1rem">
      <img :src="imgBlue" class="right-first-blue" />
      <!-- 红色背景 -->
      <div class="right-first-progress">
        <!-- 蓝色进度条 -->
        <div class="right-first-progress-local" :style="{'width': data * 30 + 'rem'}"></div>
      </div>
      <img :src="imgRed" class="right-first-red" />
    </div>
    <div style="width:90%;margin:0.5rem auto">
      <div class="right-first-left-title right-first-left-font">
        总体完成进度
        <span class="right-first-left-font-blue">{{data * 100}}</span>%
      </div>
      <div class="right-first-right-title right-first-left-font">
        未完成
        <span class="right-first-left-font-red">{{100-data * 100}}</span>%
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["data"],
  data() {
    return {
      imgBlue: require("../../assets/right/first/icon_blue.png"),
      imgRed: require("../../assets/right/first/icon_red.png")
    };
  }
};
</script>
<style>
.right-first-root {
  position: relative;
  width: 100%;
}
.right-first-blue {
  display: inline-block;
  width: 1rem;
  height: 1rem;
}
.right-first-red {
  display: inline-block;
  width: 1rem;
  height: 1rem;
}
.right-first-progress {
  display: inline-block;
  width: 30rem;
  height: 1rem;
  margin: 0 0.5rem;
  background-image: linear-gradient(
    270deg,
    #d94f64 0%,
    rgba(217, 79, 100, 0.2) 100%
  );
  border-radius: 0.3rem;
  border-radius: 0.3rem;
}
.right-first-progress-local {
  display: inline-block;
  width: 10rem;
  height: 1rem;
  background-image: linear-gradient(
    270deg,
    #2bb7ff 0%,
    rgba(43, 212, 255, 0.2) 100%
  );
  border-radius: 0.3rem;
  border-radius: 0.3rem;
}
.right-first-left-font {
  font-family: PingFangSC-Regular;
  font-size: 0.9rem;
  color: #bed7fa;
  letter-spacing: 0;
}
.right-first-left-title {
  display: inline-block;
  width: 50%;
  text-align: start;
}
.right-first-right-title {
  display: inline-block;
  width: 50%;
  text-align: end;
}
.right-first-left-font-blue {
  font-family: DINAlternate-Bold;
  font-size: 1.3rem;
  /* color: #2bb7ff; */
  color:white;
  letter-spacing: 0;
}
.right-first-left-font-red {
  font-family: DINAlternate-Bold;
  font-size: 1.3rem;
  color: #d84e63;
  letter-spacing: 0;
}
</style>