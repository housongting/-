<template>
  <div class="login">
    <el-form :model="formData" :rules="rules" ref="ruleForm">
      <el-form-item prop="username">
        <el-input v-model="formData.username" size="middle" prefix-icon="el-icon-s-custom" placeholder="请输入账号"></el-input>
      </el-form-item>
      <el-form-item prop="password">
        <el-input v-model="formData.password" size="middle" prefix-icon="el-icon-lock" show-password placeholder="请输入密码"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="loginIn('ruleForm')">登
          <span style="width:50px;display:inline-block"></span>录
        </el-button>
      </el-form-item>
      <p style="color:#DCDFE6;">admin <span style="width:10px;display:inline-block"></span>管理员<br>staff<span style="width:10px;display:inline-block"></span>成员</p>
    </el-form>
  </div>
</template>

<script>
import { initDynamicRoutes } from "../../router/index.js";
export default {
  name: "login",
  data () {
    return {
      formData: {
        username: "",
        password: ""
      },
      rules: {
        username: [{ required: true, message: "请输入账号", trigger: "blur" }],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }]
      }
    };
  },
  mounted () { },
  methods: {
    loginIn (formName) {
      var that = this;
      this.$refs[formName].validate(valid => {
        //验证通过
        if (valid) {
          //管理员
          if (this.formData.username == "admin") {
            that.axios
              .get("http://localhost:8080/static/json/login.json")
              .then(function (res) {
                var responData = res.data.data;
                sessionStorage.setItem("token", responData[0].admin.token); //用于路由导航守卫
                that.$store.commit("setUsername", responData[0].admin.username);
                that.$store.commit("setMenuList", responData[0].admin.menu);
                initDynamicRoutes(); //调用router文件夹的index.js方法，动态添加路由
                that.$router.push({ path: "/home" });
                that.$message({
                  message: '恭喜你，登录成功！',
                  type: 'success',
                  duration: 1000
                });
              });
            //员工
          } else if (this.formData.username == "staff") {
            that.axios
              .get("http://localhost:8080/static/json/login.json")
              .then(function (res) {
                var responData = res.data.data;
                sessionStorage.setItem("token", responData[1].staff.token); //用于路由导航守卫
                that.$store.commit("setUsername", responData[1].staff.username);
                that.$store.commit("setMenuList", responData[1].staff.menu);
                initDynamicRoutes(); //调用router文件夹的index.js方法，动态添加路由
                that.$router.push({ path: "/home" });
                that.$message({
                  message: '恭喜你，登录成功！',
                  type: 'success',
                  duration: 1000
                });
              });
          } else {
            that.$message.error({
              message: "未注册成为用户，请更换账号！",
              duration: 1000
            });
            return false;
          }
        } else {
          that.$message.error({
            message: "请检查账号，密码是否正确！",
            duration: 1000
          });
          return false;
        }
      });
    }
  }
};
</script>

<style lang="scss" scoped>
@import "./login.scss";
</style>>

