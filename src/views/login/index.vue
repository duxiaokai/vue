<template>
  <div class="login">
    <el-card class="card">
      <div class="logo">
        <img src="../../assets/img/logo_index.png" alt />
      </div>
      <!-- 绑定表单 -->
      <el-form ref="loginForm" :model="loginForm" :rules="ruless" style="margin-top:20px">
        <el-form-item prop="mobile">
          <!-- 绑定手机号 -->
          <el-input v-model="loginForm.mobile" placeholder="请输入手机号"></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <!-- 绑定验证码 -->
          <el-input v-model="loginForm.code" style="width:250px" placeholder="请输入验证码"></el-input>
          <el-button style="float:right">点击获取验证码</el-button>
        </el-form-item>
        <el-form-item prop="check">
          <!-- 绑定协议 -->
          <el-checkbox v-model="loginForm.check">我已阅读并同意"用户隐私条款"</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button  @click="login" style="width:100%" type="primary">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    let validator = function(rule, value, callBack) {
      if (value) {
        callBack();
      } else {
        callBack(new Error("如不勾选用户协议见无法进入"));
      }
    };
    return {
      loginForm: {
        mobile: "", //手机号
        code: "", //验证码
        check: false //用户协议
      },
      // 校验程序
      ruless: {
        mobile: [
          {
            required: true,
            message: "请填写手机号"
          },
          {
            pattern: /^1[3456789]\d{9}$/,
            message: "请正确填写11位中国手机号"
          }
        ],
        code: [
          {
            required: true,
            message: "验证码不能为空"
          },
          {
            pattern: /^\d{6}$/,
            message: "请正确填写6位验证码"
          }
        ],
        check: [{
          validator
        }]
      }
    }
  },
  methods: {
    login () {
      //通过el-form校验整个表单
      this.$refs.loginForm.validate((isOk=>{
        
      })
    }
  }
};
</script>

<style lang = 'less' scoped>
/* //less写法 scoped知针对当前样式 */
.login {
  background: url("../../assets/img/login_bg.jpg");
  height: 100vh;
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
  .card {
    width: 440px;
    height: 350px;
    .logo {
      text-align: center;
      img {
        height: 45px;
      }
    }
  }
}
</style>