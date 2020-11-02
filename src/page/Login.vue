<template>
    <div class="login-box">
        <div class="header">
            <img src="../assets/icon.png">
            <span>聚牛策</span>
            <img src="../assets/user.png">
            <span>1549****5533</span>
        </div>
        <div class="content">
            <p>AI量化交易</p>
            <p>智能交易助手 解决人工交易的烦恼</p>
            <p>简单易用的操作界面 0基础入门</p>
            <button @click="login">进入后台</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Login',
        methods: {
            login() {
                this.$router.back()
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
    }
    .header{
        height: 61px;
        display: flex;
        align-items: center;
        background: rgba(255,255,255,.54);
        box-shadow: 0px 3px 6px rgba(172, 172, 172, 0.16);
        padding: 0 10% 0;
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
        margin-left: 10%;
        margin-top: 141px;
        p {
            &:first-child{
                font-size: 67px;
                color: #0F0F0F;
                font-weight: bold;
                margin-bottom: 23px;
            }
            &:nth-child(2){
                color: #5F5F5F;
                font-size: 24px;
                margin-bottom: 1px;
            }
            &:nth-child(3){
                color: #5F5F5F;
                font-size: 24px;
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
</style>
