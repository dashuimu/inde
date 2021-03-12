<template>
    <div class="login">
        <el-card class="login-card">
            <div class="login-img">
                <img src="../../assets/img/logo_index.png" alt="">
            </div>
            <el-form class="login-form">
                <el-form-item >
                     <el-input placeholder="请输入手机号"></el-input>
                </el-form-item>
                <el-form-item >
                    <el-input placeholder="验证码" style="width:60%"></el-input>
                    <el-button style="width:35%;float:right">发送验证码</el-button>
                </el-form-item>
                <el-form-item style="margin-top:-15px">
                        <el-checkbox label="我已阅读并同意用户协议和隐私条款"></el-checkbox>
                </el-form-item>
                <el-form-item style="margin-top:-20px">
                    <el-button type="primary" style="width:100% ">登录</el-button>
                </el-form-item>
            </el-form>
        </el-card>
    </div>
</template>
<script>
export default {}
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
