<template>
  <div>
    <ul class="year_zps_ul">
      <li :class="year%4===0 ? 'year_zps_li':''">2019</li>
      <li :class="year%4===1 ? 'year_zps_li':''">2018</li>
      <li :class="year%4===2 ? 'year_zps_li':''">2017</li>
      <li :class="year%4===3 ? 'year_zps_li':''">2016</li>
    </ul>
  </div>
</template>
<script>
export default {
  props: ["year"]
};
</script>
<style lang="scss">
.year_zps_ul {
  display: flex;
  margin-top: 1.85rem;
  margin-right: 1.54rem;
  margin-bottom: 1.5rem;
  li {
    text-align: center;
    border: 1px solid #1856fd;
    width: 3.07rem;
    height: 1.85rem;
    font-size: 0.92rem;
    line-height: 1.85rem;
    text-align: center;
    color: #bed7fa;
  }
}

.year_zps_li {
  background: #0349a9;
}
</style>