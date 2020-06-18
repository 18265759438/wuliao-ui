<template>
  <el-col :span="12">
    <el-menu
      default-active="1"
      class="el-location-vertical-demo"
      @open="handleOpen"
      @close="handleClose"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b" router
    >
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span slot="title">采购价格看板管理</span>
        </template>
        <el-menu-item-group>
          <el-menu-item index="/Home/">发布物料</el-menu-item>
          <el-menu-item index="/Home/userManagement">物料管理</el-menu-item>
        </el-menu-item-group>
        <el-menu-item-group>
          <el-menu-item index="">报价看板</el-menu-item>
        </el-menu-item-group>
       <el-menu-item-group>
          <el-menu-item index="">购物车</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-menu-item index="2">
        <i class="el-icon-menu"></i>
        <span slot="title">商品管理</span>
      </el-menu-item>
      <el-menu-item index="3">
        <i class="el-icon-document"></i>
        <span slot="title">订单管理</span>
      </el-menu-item>
      <el-menu-item index="4">
        <i class="el-icon-setting"></i>
        <span slot="title">收藏管理</span>
      </el-menu-item>
      <el-menu-item index="4">
        <i class="el-icon-setting"></i>
        <span slot="title">企业信息</span>
      </el-menu-item>
      <el-menu-item index="4">
        <i class="el-icon-setting"></i>
        <span slot="title">注册开户</span>
      </el-menu-item>
      <el-menu-item index="4">
        <i class="el-icon-setting"></i>
        <span slot="title">支付管理</span>
      </el-menu-item>
    </el-menu>
  </el-col>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>

<style scoped>
*{
    margin: 0;
    padding: 0;
}
.el-menu{
    overflow: hidden;
}
.el-col-12{
    width: 14%;
    height: 969px;
}
.el-menu{
    height: 100%;
}
</style>