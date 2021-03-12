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
      this.$refs.myForm.validate(function (isOK) {
        if (isOK) {
          console.log('校验成功')
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
