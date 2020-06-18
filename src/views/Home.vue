<template>
  <div class="home">
    <qnav></qnav>
    <qheader></qheader>
    <qcenter></qcenter>
  </div>
</template>

<script>
// @ is an alias to /src
import qnav from '@/components/qnav.vue'
import qheader from '@/components/qheader.vue'
import qcenter from '@/components/qcenter.vue'


export default {
  name: 'home',
  components: {
    qnav,
    qheader,
    qcenter
  }
}
</script>

<style scoped>
.el-col-12{
  position: fixed;
  left: 0;
  top: 0;
  z-index: 999;
}
.main-header{
position: fixed;
top: 0;
z-index: 999;
left: 14%;
}
.center{
  /* margin-left: 14%;
  margin-top: 10%; */
  position: absolute;
  left: 14%;
  top: 12%;
  width: 86%;
}
</style>
