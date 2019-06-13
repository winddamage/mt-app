<template>
  <div>
    <el-row class="login">
      <el-col :span="12">
        <img src="//s0.meituan.net/bs/file/?f=fe-sso-fs:build/page/static/banner/www.jpg" width="480" height="370" alt="美团网">
      </el-col>
      <el-col :span="12">
        <el-form class="login-form">
          <p>
            <span>账号登录</span>
          </p>
          <el-form-item>
            <el-input
              placeholder="账号"
              v-model="name">
              <i slot="prefix" class="el-input__icon el-icon-user"></i>
            </el-input>
          </el-form-item>
          <el-form-item>
            <el-input
              type="password"
              placeholder="密码"
              v-model="pwd">
              <i slot="prefix" class="el-input__icon el-icon-unlock"></i>
            </el-input>
          </el-form-item>
          <p class="forget-pwd">
            <a href="#">忘记密码</a>
          </p>
          <el-form-item>
            <el-button class="btn-block" @click="login">登录</el-button>
          </el-form-item>
          <p>
            还没有账号？<nuxt-link to="/register">免费注册</nuxt-link>
          </p>
        </el-form>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: 'Login',
  layout: 'blank',
  data () {
    return {
      name: '',
      pwd: ''
    }
  },
  methods: {
    login () {

    }
  }
}
</script>

<style lang="scss">
.login {
  width: 70%;
  margin: 0 auto;
  padding: 30px 0;
  .login-form {
    width: 70%;
    margin: 0 auto;
    .el-form-item {
      .btn-block {
        width: 100%;
        background-color: #2eb7aa;
        color: #fff;
        border: 0;
        border-bottom: 1px solid #008177;
        letter-spacing: 2px;
      }
    }
    .forget-pwd {
      text-align: right;
    }
  }
}
</style>
