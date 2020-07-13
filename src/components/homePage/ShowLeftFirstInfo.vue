<template>
  <div style="position:absolute;">
    <div id="left-first-info-template-root"></div>
    <div class="left-first-info-title">
      {{title}}
      <br />
      {{unit}}
    </div>
    <div class="left-first-info-data">{{data}}</div>
    <div :class="[{'is-data-down': !isUP}, {'is-data-up': isUP} , 'left-first-info-prenct']">同比：{{periodofyear}}%</div>
  </div>
</template>
<script>
export default {
  props: ["title", "data", "unit", "periodofyear"],
  computed: {
    isUP: function() {
      if(this.periodofyear > 0){
        return true
      } else {
        return false
      }
    }
  }
};
</script>
<style>
#left-first-info-template-root {
  display: inline-block;
  width: 6.4rem;
  height: 6.4rem;
  background-color: transparent;
  border: 0.2rem solid #04a0fe;
  border-radius: 3.2rem;
  position: absolute;
  -webkit-box-shadow: inset 0 1px 7px 0 #04a0fe;
  box-shadow: inset 0 1px 7px 0 #04a0fe;
  clip: rect(0px, 7rem, 5.3rem, 0px);
}
.left-first-info-title {
  position: absolute;
  width: 4rem;
  height: 4rem;
  margin-top: 1.5rem;
  margin-left: 1.1rem;
  font-size: 0.9rem;
  /* color: #bed7fa; */
  color: white;
  letter-spacing: 0;
  text-align: center;
  line-height: 1rem;
}
.left-first-info-data {
  width: 6.4rem;
  text-align: center;
  position: absolute;
  top: 4.8rem;
  font-family: DINAlternate-Bold;
  font-size: 1.1rem;
  /* color: #2ab3fa; */
  color: white;
  letter-spacing: 0;
  text-shadow: 0 0 0.1rem #000000;
}
.left-first-info-prenct {
  width: 6.4rem;
  text-align: center;
  position: absolute;
  top: 6rem;
  opacity: 0.8;
  font-family: PingFangSC-Regular;
  font-size: 0.8rem;
  letter-spacing: 0;
}

</style>