<template>
    <div class="login">
        <el-card class="login-card">
            <div class="login-img">
                <img src="../../assets/img/logo_index.png" alt="">
            </div>
            <el-form class="login-form" :model="loginForm" :rules="loginRules" ref="myForm">
                <el-form-item prop="mobile">
                     <el-input  placeholder="请输入手机号" v-model="loginForm.mobile"></el-input>
                </el-form-item>
                <el-form-item prop="code">
                    <el-input v-model="loginForm.code" placeholder="验证码" style="width:60%" ></el-input>
                    <el-button style="width:35%;float:right">发送验证码</el-button>
                </el-form-item>
                <el-form-item style="margin-top:-15px" prop="agree" >
                        <el-checkbox v-model="loginForm.agree">我已阅读并同意<a href="" style="color:#3296FA">用户协议</a>和<a href="" style="color:#3296FA">隐私条款</a></el-checkbox>
                </el-form-item>
                <el-form-item style="margin-top:-10px">
                    <el-button @click="loginD" type="primary" style="width:100% ">登录</el-button>
                </el-form-item>
            </el-form>
        </el-card>
    </div>
</template>
<script>
export default {
  data () {
    var validator = function (rule, value, callback) {
      if (value) {
        callback()
      } else {
        callback(new Error('你必须勾选'))
      }
    }
    return {
      loginForm: {
        mobile: '',
        code: '',
        agree: false
      },
      loginRules: {
        mobile: [
          { required: true, message: '请不要空白', trigger: 'blur' },
          { pattern: /^1[3456789]\d{9}$/, message: '请输入正确的手机号', trigger: 'blur' }
        ],
        code: [
          { required: true, message: '请不要空白', trigger: 'blur' },
          { pattern: /^\d{6}$/, message: '请输入正确的验证码' }
        ],
        agree: [
          {
            validator
          }
        ]
      }
    }
  },
  methods: {
    loginD () {
      // ref 被用来给DOM元素或子组件注册引用信息。引用信息会根据父组件的 $refs 对象进行注册。如果在普通的DOM元素上使用，引用信息就是元素; 如果用在子组件上，引用信息就是组件实例
      // 注意：只要想要在Vue中直接操作DOM元素，就必须用ref属性进行注册
      this.$refs.myForm.validate((isOK) => {
        if (isOK) {
          // 只有一切校验通过之后，才会进行网络请求
          this.$axios({
            method: 'post',
            url: '/authorizations',
            data: this.loginForm
          }).then(result => {
            // 将后台返回的token令牌存储到前端缓存中
            window.localStorage.setItem('user-token', result.data.data.token)
            // 跳转到主页
            this.$router.push('/home')
          }).catch(() => {
            this.$message({
              // 消息提示，登陆不成功
              message: '警告哦，登录不成功',
              type: 'warning'
            })
          })
        }
      })
    }
  }
}

</script>

<style lang="less">
.login{
    background-image: url('../../assets/img/login_bg.jpg');
    height: 100vh;
    background-size: cover;
    display: flex;
    justify-content: center;
    align-items: center;
    .login-card{
        height: 360px;
        width: 580px;
        .login-img{
            text-align: center;
            img{
                height: 50px;
                margin-top: 10px;
            }
        }
        .login-form{
            padding: 30px 30px 0 30px ;
        }
    }
}
</style>
