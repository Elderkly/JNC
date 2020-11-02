<template>
    <div class="login-box">
        <div class="header">
            <img src="../assets/icon.png">
            <span>聚牛策</span>
            <div v-show="login" @click="showVip = !showVip,showShade = false">
                <img src="../assets/user.png" >
                <span>1549****5533</span>
                <div class="vip-box" v-show="showVip">
                    <p>会员剩余天数</p>
                    <p>128</p>
                    <button @click.stop="showShade = !showShade">续费</button>
                </div>
            </div>
        </div>
        <div class="content" v-if="login">
            <p>AI量化交易</p>
            <p>智能交易助手 解决人工交易的烦恼</p>
            <p>简单易用的操作界面 0基础入门</p>
            <button @click="">进入后台</button>
        </div>
        <div class="content" v-else>
            <div class="login">
                <p>手机登入</p>
                <p>为注册的手机号，请选注册</p>
                <input type="text" placeholder="手机号码" v-model="userName">
                <input type="password" placeholder="密码" v-model="passWord">
                <p @click="register = true">注册新账号</p>
                <button @click="_login">登入</button>
            </div>
        </div>
        <div class="content register" v-show="register">
            <div>
                <p>手机号注册</p>
                <p>为注册的手机号，请选注册</p>
                <input type="text" placeholder="手机号码" v-model="registerData.userName">
                <input type="password" placeholder="密码" v-model="registerData.passWord">
                <input type="password" placeholder="确认密码" v-model="registerData._passWord">
                <div class="code">
                    <input type="text" placeholder="验证码" v-model="registerData.code">
                    <span>发送验证码</span>
                </div>
                <button @click="_register">注册</button>
            </div>
        </div>
        <div class="showShade" v-show="showShade">
            <div>
                <img src="../assets/QRCode.png"/>
                <p>2999元/年</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Login',
        data() {
            return {
                login: !!localStorage.getItem('USERINFO'),
                userName: null,
                passWord: null,
                register: false,
                registerData: {
                    userName: null,
                    passWord: null,
                    _passWord: null,
                    code: null
                },
                showVip: false,
                showShade: false
            }
        },
        methods: {
            _login() {
                const {userName, passWord} = this
                const text = !userName ? '请输入用户名'
                    :  !passWord ? '请输入密码'
                        : null
                if (!text) {
                    localStorage.setItem("USERINFO",JSON.stringify({userName: this.userName}))
                    // this.$router.back()
                    this.login = true
                } else {
                    alert(text)
                }
            },
            _register() {
                const {userName, passWord, _passWord, code} = this.registerData
                const text = !userName ? '请输入用户名'
                    :  !passWord || !_passWord ? '请输入密码和确认密码'
                        : !code ? '请输入验证码'
                            : passWord !== _passWord ? '两次密码不一致'
                                : null
                if (!text) {
                    localStorage.setItem("USERINFO",JSON.stringify({userName: this.registerData.userName}))
                    this.login = true
                    this.register = false
                } else {
                    alert(text)
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .login-box{
        width: 100%;
        height: 100vh;
        background-image: url("../assets/bg.png");
        background-size: 100% 100%;
        position: relative;
        overflow: hidden;
    }
    .header{
        height: px2Rem(61px);
        display: flex;
        align-items: center;
        background: rgba(255,255,255,.54);
        box-shadow: 0px 3px 6px rgba(172, 172, 172, 0.16);
        padding: 0 px2Rem(268px) 0;
        box-sizing: border-box;
        position: relative;
        z-index: 10;
        &>img:first-child{
            width: 33px;
        }
        &>div{
            cursor: pointer;
            position: relative;
            img{
                width: 13px;
            }
            span{
                font-size: 12px;
                color: #808080;
                margin-left: 3px;
            }
        }
        &>span:nth-child(2){
            font-size: 19px;
            color: #0A1832;
            font-weight: 500;
            margin-left: 6px;
            flex: 1;
            text-align: left;
        }
    }
    .content{
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin-left: px2Rem(268px);
        margin-top: px2Rem(141px);
        p {
            &:first-child{
                font-size: px2Rem(67px);
                color: #0F0F0F;
                font-weight: bold;
                margin-bottom: px2Rem(23px);
            }
            &:nth-child(2){
                color: #5F5F5F;
                font-size: px2Rem(24px);
                margin-bottom: 1px;
            }
            &:nth-child(3){
                color: #5F5F5F;
                font-size: px2Rem(24px);
            }
        }
        button{
            width: 261px;
            height: 57px;
            border-radius: 4px;
            background: rgb(85,189,103);
            color: #fff;
            font-size: 24px;
            text-align: center;
            line-height: 57px;
            margin-top: 63px;
            border: none;
            cursor: pointer;
        }
    }
    .login{
        width: px2Rem(442px);
        height: px2Rem(547px);
        background: #fff;
        border-radius: 12px;
        position: absolute;
        right: px2Rem(380px);
        top: 20%;
        box-shadow: 0px 2px 4px rgba(165, 165, 165, 0.16);
        padding: px2Rem(71px) px2Rem(48px) 0 px2Rem(70px);
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        align-items: center;
        p {
            &:first-child{
                font-size: px2Rem(22px);
                color: #1966FF;
                margin-bottom: 0;
                font-weight: 400;
            }
            &:nth-child(2) {
                font-size: px2Rem(12px);
                color: #B4B4B4
            }
            &:nth-child(5) {
                font-size: px2Rem(12px);
                color: #1966FF;
                text-align: right;
                width: 100%;
                margin-top: px2Rem(12px);
                cursor: pointer;
            }
        }
        button{
            width: px2Rem(324px);
            height: px2Rem(57px);
            border-radius: 4px;
            background: #ee6c5b;
            color: #fff;
            font-size: px2Rem(24px);
            text-align: center;
            line-height: px2Rem(57px);
            margin-top: px2Rem(48px);
            border: none;
            cursor: pointer;
        }
    }
    input {
        margin-top: px2Rem(28px);
        height: px2Rem(51px);
        border: 1px solid #EAEAEA;
        width: 100%;
        border-radius: 6px;
        text-indent: px2Rem(20px);
        outline-color: rgba(25, 102, 255, .8);
        line-height: px2Rem(51px);
        font-size: px2Rem(23px);
        &::-webkit-input-placeholder{
            color: rgba(180, 180, 180, .2) !important;
            font-size: px2Rem(23px);
            font-weight: 300;
        }
    }
    .register{
        height: 100vh;
        padding-top: px2Rem(61px);
        background: #fff;
        position: absolute;
        width: 100%;
        top: 0;
        left: 0;
        margin: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        &>div{
            width: px2Rem(324px);
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: px2Rem(-80px);
            p:first-child{
                font-size: px2Rem(22px);
                color: #1966FF;
                margin-bottom: 0;
                font-weight: 400;
            }
            p:nth-child(2) {
                font-size: px2Rem(12px);
                color: #B4B4B4
            }
            .code{
                position: relative;
                width: 100%;
                span{
                    position: absolute;
                    right: px2Rem(10px);
                    top: px2Rem(45px);
                    font-size: px2Rem(17px);
                    color: rgba(25, 102, 255, 1);
                    font-weight: 300;
                    cursor: pointer;
                }
            }
            button{
                width: px2Rem(324px);
                height: px2Rem(57px);
                border-radius: 4px;
                background: #ee6c5b;
                color: #fff;
                font-size: px2Rem(24px);
                text-align: center;
                line-height: px2Rem(57px);
                margin-top: px2Rem(81px);
                border: none;
                cursor: pointer;
            }
        }
    }
    .vip-box{
        position: absolute;
        width: px2Rem(120px);
        height: px2Rem(73px);
        border-radius: 10px;
        border: 1px solid rgba(239, 239, 239, 1);
        background: #fff;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 10px 0;
        right: px2Rem(-10px);
        top: px2Rem(30px);
        p:first-child{
            font-size: px2Rem(9px);
            color: rgba(183, 183, 183, 1);
        }
        P:nth-child(2) {
            font-size: px2Rem(16px);
            color: rgba(255, 107, 58, 1);
            margin: 3px 0;
        }
        button {
            border: none;
            width: px2Rem(60px);
            height: px2Rem(20px);
            background: #ee6c5b;
            color: #fff;
            font-size: 6px;
            text-align: center;
            line-height: px2Rem(20px);
            border-radius: 2px;
        }
    }
    .showShade{
        position: absolute;
        width: 100%;
        height: 100vh;
        background: rgba(0,0,0,.55);
        top: px2Rem(61px);
        display: flex;
        align-items: center;
        justify-content: center;
        &>div{
            width: px2Rem(522px);
            height: px2Rem(425px);
            background: rgba(0,0,0,.92);
            border-radius: 22px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            img{
                width: px2Rem(220px);
            }
            p{
                margin-top: px2Rem(31px);
                font-size: px2Rem(40px);
                color: rgba(255, 94, 89, 1);
            }
        }
    }
</style>
