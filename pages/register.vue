<template>
  <div>
    <article class="register-top">
      <nuxt-link to="/login">登入</nuxt-link>
    </article>
    <section class="register-form">
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="rule-form">
        <el-form-item label="昵称" prop="name">
          <el-input v-model="ruleForm.name"></el-input>
        </el-form-item>
        <el-form-item label="邮箱" prop="email">
          <el-input v-model="ruleForm.email"></el-input>
          <el-button size="mini" round @click="sendMsg">发送验证码</el-button>
          <span class="status">{{statusMsg}}</span>
        </el-form-item>
        <el-form-item label="验证码" prop="code">
          <el-input v-model="ruleForm.code" maxlength="4"></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="pwd">
          <el-input v-model="ruleForm.pwd" type="password"></el-input>
        </el-form-item>
        <el-form-item label="确认密码" prop="cppwd">
          <el-input v-model="ruleForm.cppwd" type="password"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="register">同意以下协议并注册</el-button>
          <div class="error">{{ errorMsg }}</div>
        </el-form-item>
        <el-form-item>
          <a href="">《美团网用户协议》</a>
        </el-form-item>
      </el-form>
    </section>
  </div>
</template>

<script>
export default {
  name: 'Register',
  layout: 'blank',
  data () {
    return {
      statusMsg: '',
      errorMsg: '',
      ruleForm: {
        name: '',
        code: '',
        email: '',
        pwd: '',
        cppwd: ''
      },
      rules: {
        name: [
          { required: true, type: 'string', message: '请输入昵称', trigger: 'blur' },
          { min: 3,  message: '长度大于 3 个字符', trigger: 'blur' }
        ],
        email: [
          { required: true, message: '请输入邮箱', trigger: 'blur' },
          { type: 'email', message: '邮箱格式不正确！', trigger: 'blur' }
        ],
        code: [
          { required: true, message: '请输入验证码', trigger: 'blur' }
        ],
        pwd: [
          { required: true, type: 'string', message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 8, message: '长度在 6-8 个字符', trigger: 'blur' }
        ],
        cppwd: [
          { required: true, type: 'string', message: '请输入密码', trigger: 'blur' },
          {
            validator: (rule, value, callback) => {
              if (value === '') {
                callback(new Error('请确认密码'))
              } else if (value !== this.ruleForm.pwd) {
                callback(new Error('两次密码不一致！'))
              } else {
                callback()
              }
            }
          }
        ]
      }
    }
  },
  methods: {
    sendMsg () {
      const self = this
      let namePass
      let emailPass
      if (self.timerId) {
        return false
      }
      this.$refs['ruleForm'].validateField('name', (valid) => {
        namePass = valid
      })
      self.statusMsg = ''
      if (namePass) {
        return false
      }
      this.$refs['ruleForm'].validateField('email', (valid) => {
        emailPass = valid
      })
      if (!namePass && !emailPass) {
        self.$axios.post('/users/verify', {
          username: encodeURIComponent(self.ruleForm.name),
          email: self.ruleForm.email
        }).then(({ status, data }) => {
          if (status === 200 && data && data.code === 0) {
            let count = 60
            self.statusMsg = `验证码已发送，剩余${count--}秒`
            self.timerId = setInterval(function () {
              self.statusMsg = `验证码已发送，剩余${count--}秒`
              if (count === 0) {
                self.statusMsg = ''
                clearInterval(self.timerId)
              }
            }, 1000)
          } else {
            self.statusMsg = data.msg
          }
        })
      }
      
    },
    register () {

    }
  }
}
</script>

<style lang="scss">
.register-top {
  height: 39px;
  line-height: 39px;
  padding: 10px;
  border-bottom: 2px solid #2bb8aa;
}
.register-form {
  width: 70%;
  padding: 30px 0;
  margin: 0 auto;
  .rule-form {
    width: 50%;
  }
}
</style>
