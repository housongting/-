<template>
  <div class="p-15 bg-color">
    <div class="bg-white p-3">
      <div class="content">
        <div class="form_box">
          <div class="input_box">
            <label>模板管理</label>
            <el-input size="medium" v-model="queryData.DsName" placeholder="数据源名称"></el-input>
          </div>
          <div class="input_box">
            <label>报表大类:</label>
            <el-select v-model="queryData.DbType" placeholder="请选择" size="medium">
              <el-option label="MSSql" value=1></el-option>
              <el-option label="Oracle" value=2></el-option>
              <el-option label="Api" value=4></el-option>
            </el-select>
          </div>
          <div class="input_box">
            <label>报表细类:</label>
            <el-select v-model="queryData.DbType" placeholder="请选择" size="medium">
              <el-option label="MSSql" value=1></el-option>
              <el-option label="Oracle" value=2></el-option>
              <el-option label="Api" value=4></el-option>
            </el-select>
          </div>
          <div class="input_box">
            <label>创建者:</label>
            <el-input size="medium" v-model="queryData.DsName" placeholder="数据源名称"></el-input>
          </div>
          <div class="input_box">
            <label>状态:</label>
            <el-select v-model="queryData.DsStatus" placeholder="请选择" size="medium">
              <el-option label="全部" value='2'></el-option>
              <el-option label="空闲" value='0'></el-option>
              <el-option label="启用" value='1'></el-option>
            </el-select>
          </div>
          <span class="btn-box">
            <button class="btn btn-1">查询</button>
            <button class="btn btn-2">重置</button>
          </span>
        </div>
        <div class="slide_btn"></div>
      </div>
    </div>
    <div class="bg-white p-3 mt-3">
      <div class="content">
        <div class="tag-box mb-3">
          <div class="tag edit"><img src="/static/imgs/add.png">新增</div>
          <div class="tag edit"><img src="/static/imgs/edit.png">修改</div>
          <div class="tag detel"><img src="/static/imgs/detel.png">删除</div>
          <span>
            总计<span>25</span>条数据
            每页显示
            <el-select v-model="queryData.selectNum" placeholder="请选择" size="medium" style="width:90px">
              <el-option label="10" value="10"></el-option>
              <el-option label="20" value="20"></el-option>
              <el-option label="30" value="30"></el-option>
            </el-select>
            条
          </span>
        </div>
        <el-table :data="tableData" border style="width: 100%">
          <el-table-column type="index" width="50" label="序号" fixed align="center"></el-table-column>
          <el-table-column prop="DsName" label="数据源名称" fixed align="center"></el-table-column>
          <el-table-column prop="DbHost" label="服务器地址" align="center"></el-table-column>
          <el-table-column prop="DbInst" label="数据库名称" align="center"></el-table-column>
          <el-table-column prop="DbHandle" label="内部名称" align="center"></el-table-column>
          <el-table-column prop="MainCategoryName" label="报表大类" align="center"></el-table-column>
          <el-table-column prop="SubCategoryName" label="报表细类" align="center"></el-table-column>
          <el-table-column label="数据源类型" align="center">
            <template slot-scope="scope">
              <span v-if="scope.row.DbMode==1">表</span>
              <span v-if="scope.row.DbMode==2">视图</span>
              <span v-if="scope.row.DbMode==3">存储过程</span>
              <span v-if="scope.row.DbMode==4">接口</span>
            </template>
          </el-table-column>
          <el-table-column label="状态" align="center">
            <template slot-scope="scope">
              <span v-if="scope.row.DsStatus==0">空闲</span>
              <span v-if="scope.row.DsStatus==1">启用</span>
            </template>
          </el-table-column>
        </el-table>
        <div class="page_box pt-2 pb-3">
          <span>
            共计<span>25</span>页
            当前位于<span>1</span>页
          </span>
          <span>
            <img src="/static/imgs/prev1.png">
            <img src="/static/imgs/prev.png">
            <img src="/static/imgs/next.png">
            <img src="/static/imgs/next1.png">
          </span>
          <span>
            跳转至
            <input type="text" />
            页
            <h3>GO</h3>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'templateManage',
  data () {
    return {
      //查询条件(DsStatus: -1表示全部)
      queryData: {
        selectNum: "10",
        DsName: '',
        DbHost: '',
        DbInst: '',
        DbType: null,
        DbMode: null,
        MainCategory: null,
        SubCategory: null,
        Descriptor: '',
        DsStatus: -1,
        DbHandle: ''
      },
      arr: ['1', 2, 3, 4],
      //查询条件默认值、静态源
      queryDefault: {
        MainCategories: ["微信", "pc"],
        SubCategories: ["报表一", "报表二"],
      },
      tableData: [
        {
          DbHandle: "dbo.sp_selectAuthClient",
          DbHost: "192.168.4.195",
          DbInst: "cmict",
          DbMode: 3,
          DbPwd: "wlzx87811024",
          DbType: 1,
          DbUser: "sa",
          Descriptor: "",
          DsId: 2,
          DsName: "sql存储过程",
          DsStatus: 1,
          MainCategory: 1,
          MainCategoryName: "微信",
          SubCategory: 11,
          SubCategoryName: null,
        },
        {
          DbHandle: "dbo.Sys_Param",
          DbHost: "192.168.4.195",
          DbInst: "cmict",
          DbMode: 1,
          DbPwd: "wlzx87811024",
          DbType: 1,
          DbUser: "sa",
          Descriptor: "",
          DsId: 1007,
          DsName: "test",
          DsStatus: 1,
          MainCategory: 1,
          MainCategoryName: "微信",
          SubCategory: 11,
          SubCategoryName: null,
        },
        {
          DbHandle: "Cmict.Wx.Data.TruckDtAdapter",
          DbHost: "",
          DbInst: "Cmict.Wx.Data.Api",
          DbMode: 4,
          DbPwd: "",
          DbType: 4,
          DbUser: "",
          Descriptor: "",
          DsId: 2013,
          DsName: "wx单箱",
          DsStatus: 0,
          MainCategory: 1,
          MainCategoryName: "微信",
          SubCategory: 11,
          SubCategoryName: null,
        },
        {
          DbHandle: "Cmict.Wx.Data.TruckDtAdapter",
          DbHost: "",
          DbInst: "Cmict.Wx.Data.Api",
          DbMode: 4,
          DbPwd: "",
          DbType: 4,
          DbUser: "",
          Descriptor: "",
          DsId: 7,
          DsName: "Api集卡",
          DsStatus: 1,
          MainCategory: 1,
          MainCategoryName: "微信",
          SubCategory: 11,
          SubCategoryName: null,
        }
      ],
      null_data: false
      //表单静态数据
      // formDefault = {
      //   MainCategories: [],
      //   SubCategories: [],
      //   DbObjects: [],//table,views,procedure
      // },
    }
  },
  // created () {
  //   console.log($('.slide_btn'))
  // }


}
</script>

<style lang="scss" scoped>
@import "./templateManage.scss";
</style>