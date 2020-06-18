<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '' }">企业工作室</el-breadcrumb-item>
      <el-breadcrumb-item>采购报价看板管理</el-breadcrumb-item>
      <el-breadcrumb-item>物料管理</el-breadcrumb-item>
    </el-breadcrumb>
    <el-table :data="this.tableData" border style="width: 100%">
      <el-table-column fixed prop="obj.ipt1" label="应用类" width="120"></el-table-column>
      <el-table-column prop="obj1" label="物料类" width="120"></el-table-column>
      <el-table-column prop="obj.ipt2" label="物料名称" width="120"></el-table-column>
      <el-table-column prop="obj.ipt9" label="品牌" width="120"></el-table-column>
      <el-table-column prop="obj.ipt4" label="牌号" width="120"></el-table-column>
      <el-table-column prop="obj.ipt5" label="规格" width="120"></el-table-column>
      <el-table-column prop="obj.pt14" label="产地" width="120"></el-table-column>
      <el-table-column prop="obj.ipt3" label="状态" width="120"></el-table-column>
      <el-table-column fixed="right" label="操作" width="180">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="stateup(scope.$index, scope.row)">上架</el-button>
          <el-button type="text" size="small">复制物料</el-button>
          <el-button type="text" size="small" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button type="text" size="small" @click="handleAdv(scope.$index, scope.row)">详情</el-button>
          <el-button type="text" size="small" @click="deleteList(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog
      :title="title"
      :visible.sync="editFormVisible"
      :close-on-click-modal="false"
      class="edit-form"
      :before-close="handleClose"
    >
      <el-form :model="editForm" label-width="80px"  ref="editForm">
        <el-form-item label="应用类" prop="data1">
          <el-input v-model="data1" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="物料类" prop="data2">
          <el-input v-model="data2" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="物料名称" prop="data3">
          <el-input v-model="data3" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="品牌" prop="data4">
          <el-input v-model="data4" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="牌号" prop="data5">
          <el-input v-model="data5" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="规格" prop="data6">
          <el-input v-model="data6" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="产地" prop="data7">
          <el-input v-model="data7" auto-complete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click.native="handleCancel('editForm')">取消</el-button>
        <el-button v-show="btnAlert1" type="primary" @click.native="updateList('editForm')">更新</el-button>
        <el-button v-show="btnAlert2" type="primary" @click.native="addList('editForm')">添加</el-button>
      </div>
    </el-dialog>

    <!-- xiangqing -->
    <el-dialog
      :title="title"
      :visible.sync="adv"
      :close-on-click-modal="false"
      class="edit-form"
      :before-close="handleClose"
    >
      <el-form :model="editForm" label-width="80px"  ref="editForm" >
        <el-form-item label="应用类" prop="data1" >
          <el-input v-model="data1" :disabled="false"></el-input>
        </el-form-item>
        <el-form-item label="物料类" prop="data2">
          <el-input v-model="data2" auto-complete="off" :disabled="true"></el-input>
        </el-form-item>
        <el-form-item label="物料名称" prop="data3">
          <el-input v-model="data3" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="品牌" prop="data4">
          <el-input v-model="data4" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="牌号" prop="data5">
          <el-input v-model="data5" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="规格" prop="data6">
          <el-input v-model="data6" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="产地" prop="data7">
          <el-input v-model="data7" auto-complete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click.native="handleCancel('editForm')">取消</el-button>
        <!-- <el-button v-show="btnAlert1" type="primary" @click.native="updateList('editForm')">更新</el-button> -->
        <el-button v-show="btnAlert2" type="primary" @click.native="addList('editForm')">添加</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import Mock from "@/assets/mock/mock";

export default {
  data() {
    return {
      obj:"",
      data1: "",
      data2: "",
      data3: "",
      data4: "",
      data5: "",
      data6: "",
      data7: "",
      disabled:false,
      adv:false,
      state: "已下架",
      tableData: [
      ],
      editForm: {
        ipt1: "",
        obj1: ""
      },  
      editFormVisible: false,
      title: "编辑",
      btnAlert1: true,
      btnAlert2: false,
      Id: 0
    };
  },
  mounted() {
    this.getp();
    this.succ();
  },
  methods: {
    getp() {
      this.obj = this.$route.query;
      if ((this.obj==null||this.obj=="")&&(this.$route.query==null||this.$route.query=="")) {
          return
      }
      this.$store.state.TATD.push(this.obj);
      // this.tableData.push(this.obj);
    },
    handleClick(row) {
      console.log(row);
    },
    succ() {
      this.$message({
        message: "发布成功",
        type: "success"
      });
    },
    //点击关闭dialog
    handleClose(done) {
      /*done();
        location.reload();*/
      this.editFormVisible = false;
    },
    //点击取消
    handleCancel(formName) {
      this.editFormVisible = false;
    },
    //点击编辑
    handleEdit(index, row) {
      this.editFormVisible = true;
      this.btnAlert1 = true;
      this.btnAlert2 = false;
      this.editForm = Object.assign({}, row); //这句是关键！！！
      if (typeof this.$refs.editForm != "undefined")
      this.$refs.editForm.resetFields();
      this.data1 = this.tableData[0].obj.ipt1;
      this.data2 = this.tableData[0].obj1;
      this.data3 = this.tableData[0].obj.ipt2;
      this.data4 = this.tableData[0].obj.ipt9;
      this.data5 = this.tableData[0].obj.ipt4;
      this.data6 = this.tableData[0].obj.ipt5;
      this.data7 = this.tableData[0].obj.ipt14;
      console.log(this.tableData);
      // console.log(editForm.ipt1)
      this._index = index;
    },
    // 修改列表数据
    updateList() {
      //  var obj = this.$route.query;
      this.tableData[0].obj.ipt1 = this.data1;
      this.tableData[0].obj1 = this.data2;
      this.tableData[0].obj.ipt2 = this.data3;
      this.tableData[0].obj.ipt9 = this.data4;
      this.tableData[0].obj.ipt4 = this.data5;
      this.tableData[0].obj.ipt5 = this.data6;
      this.tableData[0].obj.ipt14 = this.data7;
      this.editFormVisible = false;
    },
    //点击详情
    handleAdv(index, row) {
      this.editFormVisible = true;
        // this.$refs.editForm.resetFields();
        this.title = "详情";
      this.data1 = this.tableData[0].obj.ipt1;
      this.data2 = this.tableData[0].obj1;
      this.data3 = this.tableData[0].obj.ipt2;
      this.data4 = this.tableData[0].obj.ipt9;
      this.data5 = this.tableData[0].obj.ipt4;
      this.data6 = this.tableData[0].obj.ipt5;
      this.data7 = this.tableData[0].obj.ipt14;
      // console.log(editForm.ipt1)
      this._index = index;
    },
    //删除列表
    deleteList(index) {
      this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          console.log(index);
          this.tableData.splice(index, 1);
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    },
    //上架下架
    stateup(index) {
      this.$confirm("是否上架该物料?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(() => {
          console.log(index);
          this.tableData[0].obj.ipt3 = "已上架";
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消上架"
          });
        });
    }
  }
};
</script>

<style scoped>
.el-breadcrumb {
  width: 100%;
  margin: 0 auto;
  margin-bottom: 20px;
  font-size: 18px;
  margin-top: 1%;
  height: 50px;
  border-bottom: 2px solid #f0e9e9;
}
.el-breadcrumb__item:first-child {
  margin-left: 1%;
}
.el-table--border {
  width: 70% !important;
  margin: 0 auto;
}
.el-tabs__header {
  margin: 0 auto;
  width: 94% !important;
}
/* .el-breadcrumb__inner{
  color: rgb(196, 141, 91);
}
.el-breadcrumb{
  color: rgb(196, 141, 91)!important;
} */
</style>