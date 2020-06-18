<template>
  <header class="main-header">
    <div class="left">
      <a href>产品服务</a>
      <a href>工作台</a>
      <a href class="active_a">柠檬豆</a>
    </div>
    <div class="right">
      <div class="h_r_left">
        <h2>你好！ Changer</h2>
        <a href class="gongying">切换到供应商</a>
      </div>
      <div class="h_r_middle">
        <img src="../assets/1.png" alt />
      </div>
      <div class="h_r_right">
        <template>
          <el-button type="text" @click="open2">退出</el-button>
        </template>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    open2() {
      let _this = this;
      this.$confirm("是否退出登录", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          sessionStorage.removeItem("token");
          _this.$router.push({ path: "/" });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消"
          });
        });
    }
  }
};
</script>

<style scoped>
a {
  text-decoration: none;
}
.main-header {
  width: 86%;
  height: 100px;
  border-top: 1px solid #9c9797;
  border-bottom: 1px solid #9c9797;
  background: #f5f5f5;
}
.left {
  float: left;
  height: 80px;
  padding-left: 52%;
  line-height: 80px;
  margin-top: 10px;
  border-right: 1px solid #d1cece;
}
.left a {
  font-weight: bold;
  margin: 20px;
}
.right {
  float: left;
}
.right h2 {
  color: rgb(248, 154, 66);
  margin-top: 12px;
}
.gongying {
  color: #fff;
  background: rgb(248, 154, 66);
  display: block;
  width: 180px;
  height: 40px;
  line-height: 40px;
  text-align: center;
  border-radius: 10px;
}
.h_r_left {
  height: 100px;
  float: left;
  padding-left: 20px;
}
.h_r_middle {
  width: 50px;
  height: 50px;
  margin: 25px 50px;
  border-radius: 50%;
  float: left;
}
.h_r_middle img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
}
.h_r_right {
  float: left;
  height: 100px;
  line-height: 100px;
  font-weight: bold;
}
.el-button--text {
  color: #333;
}
.el-button--text:hover {
  color: #9c9797;
}
</style>