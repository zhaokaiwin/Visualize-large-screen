<template>
  <div>
    <img :src="img" class="center-second-info-img" />
    <div class="center-second-info-word-block">
      <div class="center-second-info-title">{{title}}</div>
      <div class="center-second-info-number">
        {{number}}
        <span class="center-second-info-unit">{{unit1}}</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["img", "title", "number", "unit1"]
};
</script>
<style>
.center-second-info-img {
  display: inline-block;
  width: 2.3rem;
  height: 2.3rem;
}
.center-second-info-title {
  font-family: PingFangSC-Regular;
  font-size: 1rem;
  /* color: #bed7fa; */
  color: #2BB7FF;
  letter-spacing: 0;
  margin-left: 0.5rem;
}
.center-second-info-unit {
  font-family: PingFangSC-Regular;
  font-size: 1rem;
  /* color: #2bb7ff; */
  color:white;
  letter-spacing: 0;
  margin-left: 0.1rem;
}
.center-second-info-number {
  font-family: DINAlternate-Bold;
  font-size: 1.3rem;
  /* color: #2bb7ff; */
  color:white;
  letter-spacing: 0;
   margin-left: 0.5rem;
   margin-top: 0.3rem;
}
.center-second-info-word-block {
  display: inline-block;
}
</style>