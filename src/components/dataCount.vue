<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '' }">企业工作室</el-breadcrumb-item>
      <el-breadcrumb-item>采购报价看板管理</el-breadcrumb-item>
      <el-breadcrumb-item>发布物料</el-breadcrumb-item>
    </el-breadcrumb>
    <el-tabs v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="发布物料" name="first">
        <div class="table_1">
          <ul>
            <li>
              应 用 类
              <input
                type="text"
                v-model="formObj.ipt1"
                placeholder="请输入物料用途、使用场景"
                class="input_text1"
              />
            </li>
            <li>
              物 料 类
              <select v-model="brand">
                <option disabled="disabled" :value="null">请选择父类</option>
                <option v-for="(item, index) in product" :value="index">{{item.brand}}</option>
              </select>
              <select v-model="type">
                <option disabled="disabled" :value="null">请选择子类</option>
                <option v-for="(item, index) in typeArray" :value="index">{{item.type}}</option>
              </select>

              <select v-model="name" @click="changeloginType()">
                <option disabled="disabled" :value="null">请选择小类</option>
                <option v-for="(item, index) in nameArray" :value="item.name">{{item.name}}</option>
              </select>
            </li>
            <li>
              物 料 名 称
              <input
                type="text"
                v-model="formObj.ipt2"
                placeholder="请输入物料名称"
                class="input_text"
              />
            </li>
            <li>
              截 止 日 期
              <el-date-picker v-model="value1" type="date" class="date_ipt" placeholder="请选择截止日期"></el-date-picker>
            </li>
          </ul>
        </div>
        <div class="table_2" v-if="flag">
          <ul>
            <li>
              产 地
              <input type="text" v-model="formObj.ipt3" placeholder="请输入钢厂" class="input_text1" />
            </li>
            <li>
              牌 号
              <input type="text" v-model="formObj.ipt4" placeholder="请输入牌号" class="input_text1" />
            </li>
            <li>
              厚 度
              <input type="text" v-model="formObj.ipt5" placeholder="请输入厚度" class="input_text1" />
            </li>
            <li>
              长 度
              <input type="text" v-model="formObj.ipt6" placeholder="请输入长度" class="input_text1" />
            </li>
            <li>
              宽 度
              <input type="text" v-model="formObj.ipt7" placeholder="请输入宽度" class="input_text1" />
            </li>
            <li>
              厚 度 公 差
              <input
                type="text"
                v-model="formObj.ipt8"
                placeholder="请输入厚度公差"
                class="input_text1"
              />
            </li>
            <li>
              屈 服 强 度
              <input
                type="text"
                v-model="formObj.ipt9"
                placeholder="请输入屈服强度"
                class="input_text1"
              />
            </li>
            <li>
              拉 伸 长 度
              <input
                type="text"
                v-model="formObj.ipt10"
                placeholder="请输入拉伸长度"
                class="input_text1"
              />
            </li>
            <li>
              拉 伸 强 度
              <input
                type="text"
                v-model="formObj.ipt11"
                placeholder="请输入拉伸强度"
                class="input_text1"
              />
            </li>
            <li>
              伸 长 率
              <input
                type="text"
                v-model="formObj.ipt12"
                placeholder="请输入伸长率"
                class="input_text1"
              />
            </li>
          </ul>
        </div>
        <div class="table_3" v-if="flag">
          <ul>
            <li>
              需 求 量
              <input
                type="text"
                v-model="formObj.ipt13"
                placeholder="请填写年度总用量"
                class="input_text1"
              />
              吨
            </li>
            <li>
              交 货 地 点
              <input
                type="text"
                v-model="formObj.ipt14"
                placeholder="请输入交货地点"
                class="input_text1"
              />
            </li>

            <li>
              交 货 时 间
              <el-date-picker v-model="value2" type="date" class="date_ipt" placeholder="请输入交货时间"></el-date-picker>
            </li>
            <li>
              质 量 等 级
              <input
                type="text"
                v-model="formObj.ipt15"
                placeholder="请输入质量等级"
                class="input_text1"
              />
            </li>
            <li>
              包 装 方 式
              <input
                type="text"
                v-model="formObj.ipt16"
                placeholder="请输入包装方式"
                class="input_text1"
              />
            </li>
            <li>
              技 术 标 准
              <input
                type="text"
                v-model="formObj.ipt17"
                placeholder="请输入技术标准"
                class="input_text1"
              />
            </li>
          </ul>
        </div>
        <div class="table_4">
          <h4>结 算 方 式</h4>
          <ul>
            <li>
              <el-checkbox label="现金电汇"></el-checkbox>
            </li>
            <li>
              <el-checkbox label="承兑汇票"></el-checkbox>
            </li>
            <li>
              <el-checkbox label="预付现金"></el-checkbox>
            </li>
            <li>
              <el-checkbox label="账期"></el-checkbox>
            </li>
          </ul>
        </div>
        <div class="fabu">
          <el-button type="warning" @click="pub()">发布</el-button>
        </div>
      </el-tab-pane>
      <el-tab-pane label="批量添加" name="second">
        <h1>我是批量添加</h1>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeName: "first",
      formObj: {
        ipt1: "",
        ipt2: "",
        ipt3: "已下架",
        ipt4: "",
        ipt5: "",
        ipt6: "",
        ipt7: "",
        ipt8: "",
        ipt9: "-",
        ipt10: "",
        ipt11: "",
        ipt12: "",
        ipt13: "",
        ipt14: "",
        ipt15: "",
        ipt16: "",
        ipt17: ""
      },
      brand: null,
      type: null,
      name: null,
      error: null,
      value1: "",
      value2: "",
      flag: false,
      radio: "1",
      product: [
        {
          brand: "钢材",
          type: [
            {
              type: "iPhone",
              name: [
                {
                  name: "iPhone XS"
                },
                {
                  name: "iPhone XS MAX"
                },
                {
                  name: "iPhone XR"
                },
                {
                  name: "iPhone X"
                },
                {
                  name: "iPhone 8 Plus"
                },
                {
                  name: "iPhone 8"
                },
                {
                  name: "iPhone 7 Plus"
                },
                {
                  name: "iPhone 7"
                },
                {
                  name: "iPhone 6S Plus"
                },
                {
                  name: "iPhone 6S "
                }
              ]
            }
          ]
        }
      ],
      pickerOptions: {
        disabledDate(time) {
          return time.getTime() > Date.now();
        },
        shortcuts: [
          {
            text: "今天",
            onClick(picker) {
              picker.$emit("pick", new Date());
            }
          },
          {
            text: "昨天",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit("pick", date);
            }
          },
          {
            text: "一周前",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", date);
            }
          }
        ]
      }
    };
  },

  created: function() {},
  computed: {
    typeArray: function() {
      return this.brand !== null ? this.product[this.brand].type : null;
    },
    nameArray: function() {
      return this.type !== null && this.typeArray.length
        ? this.typeArray[this.type].name
        : null;
    }
    // check: function() {
    //   this.error = null;
    //   switch (true) {
    //     case this.brand === null:
    //       this.error = "品牌";
    //       break;
    //     case this.type === null:
    //       this.error = "产品类型";
    //       break;
    //     case this.name === null:
    //       this.error = "产品名称";
    //       break;
    //   }
    //   return this.error;
    // }
  },
  methods: {
    pub() {
      var obj = this.formObj;
      var obj1 = this.name;
      if ( this.formObj.ipt1 == null || this.formObj.ipt1 == ""&&this.formObj.ipt2 == null || this.formObj.ipt2 == ""&&this.name == null || this.name == "" && this.value1 == null||this.value1 == "") {
        alert('有的输入框为空,请检查')
      }else{
        this.$router.push({
          path: "/Home/userManagement",
          query: { obj, obj1 }
        });
      }

      // this.$confirm("确定要发布吗?", "提示", {
      //   confirmButtonText: "确定",
      //   cancelButtonText: "取消",
      //   type: "warning"
      // })
      // .then(() => {
      //   // console.log(index);
      //     this.$router.push({
      //     path: "/Home/userManagement",
      //     query: { obj, obj1 }
      //   });

      // })
      // .catch(() => {
      //   this.$message({
      //     type: "info",
      //     message: "已取消发布"
      //   });
      // });
    },
    handleClick(tab, event) {},
    changeloginType() {
      // var obj = this.product[0].type[0].name[0].name;
      // alert('as')
      // var self = this;
      // console.log(this.name)
      if (this.name == "iPhone XS") {
        this.flag = true;
      }
    }
  }
  // created(){
  //   this.changeloginType()
  // }
};
</script>

<style scoped>
.el-breadcrumb {
  width: 100%;
  margin: 0 auto;
  font-size: 18px;
  margin-top: 1%;
  height: 50px;
  border-bottom: 2px solid #d4c3c3;
}
.el-breadcrumb__item:first-child {
  margin-left: 1%;
}
.table_1 {
  width: 94%;
  background: #f5f5f5;
  margin: 0 auto;
  margin-bottom: 20px;
}
.table_1 ul li {
  height: 50px;
  line-height: 50px;
  padding-left: 2%;
  font-weight: bold;
  list-style: none;
}
.input_text1 {
  width: 300px;
  height: 40px;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  margin-left: 4.6%;
}
.input_text {
  width: 300px;
  height: 40px;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  margin-left: 3%;
}
select {
  width: 260px;
  height: 40px;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  margin-left: 4.6%;
}
.date_ipt {
  margin-left: 3%;
}
.table_2 {
  width: 94%;
  background: #f5f5f5;
  height: 260px;
  margin: 0 auto;
  margin-bottom: 20px;
}
.table_2 ul li {
  list-style: none;
  height: 50px;
  float: left;
  width: 48%;
  line-height: 50px;
  padding-left: 2%;
  font-weight: bold;
}
.table_3 {
  width: 94%;
  background: #f5f5f5;
  margin: 0 auto;
  margin-bottom: 20px;
}
.table_3 ul li {
  list-style: none;
  height: 50px;
  line-height: 50px;
  padding-left: 2%;
  font-weight: bold;
}
.fabu {
  width: 94%;
  margin: 0 auto;
  text-align: center;
  margin-bottom: 30px;
}
.table_4 {
  width: 94%;
  background: #f5f5f5;
  margin: 0 auto;
  margin-bottom: 20px;
}
.table_4 ul li {
  list-style: none;
  padding-left: 12%;
}
.table_4 h4 {
  padding-left: 2%;
}
.el-checkbox {
  font-size: 18px;
  font-weight: bold;
}
</style>