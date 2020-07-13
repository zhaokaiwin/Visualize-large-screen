<template>
  <div :class="['message-div', {'message-div-hover': isSelect}]">
    <div class="message-number">{{number}}</div>
    <div class="message-unit">{{unit}}</div>
  </div>
</template>
<script>
export default {
  props: ["number", "unit", "isSelect"]
};
</script>
<style lang="scss">
.message-div {
  width: 7.1rem;
  height: 3.6rem;
  opacity: 0.5;
  background: #00183b;
  border: 1px solid #2b88ff;
  box-shadow: inset 0 1px 7px 0 #2b83ff;

  .message-number {
    font-family: DINAlternate-Bold;
    font-size: 1.3rem;
    // color: #2bb7ff;
    color:white;
    opacity: 1;
    letter-spacing: 0.05rem;
    margin-left: 0.5rem;
    margin-top: 0.5rem;
  }

  .message-unit {
    opacity: 0.8;
    font-family: PingFangSC-Regular;
    font-size: 0.1rem;
    // color: #bed7fa;
    color:#2BB7FF;
    opacity: 1;
    letter-spacing: 0;
    margin-left: 0.5rem;
    margin-top: 0.1rem;
  }
}
.message-div-hover {
  opacity: 1;
}
</style>