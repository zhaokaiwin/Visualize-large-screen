<template>
  <div id="right-third-info-template-root">
    <div class="right-third-info-title">{{title}}</div>
    <div class="right-third-info-number">
      {{number}}
      <span class="right-third-info-unit">{{unit1}}</span>
    </div>
  </div>
</template>
<script>
export default {
  props: ["img", "title", "number", "unit1"]
};
</script>
<style>
#right-third-info-template-root {
    display: inline-block;
}
.right-third-info-title {
  font-family: PingFangSC-Regular;
  font-size: 14px;
  /* color: #bed7fa; */
  color:#2BB7FF;
  letter-spacing: 0;
  margin-left: 1rem;
  margin-bottom:0.5rem;
}
.right-third-info-unit {
  font-family: PingFangSC-Regular;
  font-size: 12px;
  /* color: #2bb7ff; */
  color:white;
  letter-spacing: 0;
  margin-left: 0.1rem;
}
.right-third-info-number {
  font-family: DINAlternate-Bold;
  font-size: 20px;
  /* color: #2bb7ff; */
  color:white;
  letter-spacing: 0;
   margin-left: 1rem;
}
</style>