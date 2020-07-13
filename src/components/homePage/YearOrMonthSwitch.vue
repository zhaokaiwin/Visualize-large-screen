<template>
  <div class="yearOrMonthSwitch">
    <div ref="year" :class="[item, {selected: year}]">本年</div>
    <div ref="month" :class="[item, {selected: !year}]">本月</div>
  </div>
</template>
<script>
export default {
  props: ["year"],
  data() {
    return {
      item: "item",
      selected: "selected"
    };
  }
};
</script>
<style lang="scss">
.yearOrMonthSwitch {
  width: 6rem;
  height: 2rem;
  background: rgba(216, 216, 216, 0);
  font-family: PingFangSC-Regular;
  position: relative;
  font-size: 12px;
  color: #ffffff;
  letter-spacing: 0;
  display: inline-block;
  border: 1px solid #0349a9;
  .item {
    width: 50%;
    height: 2rem;
    display: inline-block;
    text-align: center;
    line-height: 2rem;
  }

  .selected {
    background: #0349a9;
  }
}
</style>