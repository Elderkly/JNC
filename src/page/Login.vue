<template>
    <div class="login-box">
        <div class="header">
            <img src="../assets/icon.png">
            <span>聚牛策</span>
            <img src="../assets/user.png" v-show="login">
            <span v-show="login">1549****5533</span>
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
                <p>注册新账号</p>
                <button @click="_login">登入</button>
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
                passWord: null
            }
        },
        methods: {
            _login() {
                console.log(this.userName,this.passWord)
                localStorage.setItem("USERINFO",JSON.stringify({userName: this.userName}))
                // this.$router.back()
                this.login = true
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
    }
    .header{
        height: px2Rem(61px);
        display: flex;
        align-items: center;
        background: rgba(255,255,255,.54);
        box-shadow: 0px 3px 6px rgba(172, 172, 172, 0.16);
        padding: 0 px2Rem(268px) 0;
        box-sizing: border-box;
        img:first-child{
            width: 33px;
        }
        img:nth-child(3) {
            width: 13px;
        }
        span:nth-child(2){
            font-size: 19px;
            color: #0A1832;
            font-weight: 500;
            margin-left: 6px;
            flex: 1;
            text-align: left;
        }
        span:last-child{
            font-size: 12px;
            color: #808080;
            margin-left: 3px;
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
        input {
            margin-top: px2Rem(28px);
            height: px2Rem(51px);
            border: 1px solid #EAEAEA;
            width: 100%;
            border-radius: 6px;
            text-indent: px2Rem(20px);
            outline-color: rgba(25, 102, 255, .8);
            &::-webkit-input-placeholder{
                color: rgba(180, 180, 180, .2) !important;
                font-size: px2Rem(23px);
                font-weight: 300;
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
</style>
