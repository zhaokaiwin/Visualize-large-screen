<template>
  <div class="right-first-info-root">
    <div class="bg_color">
      <img :src="imgurl" class="img" />
    </div>
    <div class="content">
      <div class="content-title">{{title}}</div>
      <div class="content-data">{{data * 100}}%</div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["imgurl", "title", "data"]
};
</script>
<style lang='scss' >
.right-first-info-root {
  display: inline-block;
  width: 15rem;
  height: 3rem;
  .bg_color {
    border: 0.15rem solid;
    display: inline-flex;
    width: 2.4rem;
    height: 2.4rem;
    justify-content: center;
    align-items: center;
    border-radius: 1.5rem;
    border-color: #00c8ff;
    .img {
      display: inline-block;
      width: 1.5rem;
      height: 1.5rem;
    }
  }

  .content {
    display: inline-block;
    width: auto;
    height: 100%;
    margin-left: 0.5rem;
    .content-title {
      opacity: 0.6;
      font-family: PingFangSC-Regular;
      font-size: 0.9rem;
      color: #bed7fa;
      letter-spacing: 0;
    }
    .content-data {
      font-family: DINAlternate-Bold;
      font-size: 1.2rem;
      // color: #2bb7ff;
      color: white;
      letter-spacing: 0;
    }
  }
}
</style>