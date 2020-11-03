<template>
    <div class="my-task">
        <div class="select">
            <span>全部任务</span>
            <div>
                <img src="../assets/search.png">
                <input type="text" placeholder="搜索">
            </div>
        </div>
        <div class="button">
            <div
                :class="['button-items',selectIndex === index ? 'action' : '']"
                v-for="(item, index) in [{text:'运行中',number: 135},{text:'暂停中',number: 101}]"
                @click="selectIndex = index"
            >
                <span>{{item.text}}</span>
                <div>{{item.number}}</div>
            </div>
        </div>
        <div class="table">
            <div class="header">

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'MyTask',
        data() {
            return {
                selectIndex: 0
            }
        }
    }
</script>

<style lang="scss" scoped>
    .select{
        display: flex;
        align-items: center;
        span{
            font-size: px2Rem(20px);
            color: #465D91;
            font-weight: bold;
            margin-right: px2Rem(22px);
        }
        div{
            position: relative;
            img {
                width: px2Rem(19px);
                position: absolute;
                top: px2Rem(11px);
                left: px2Rem(15px);
            }
            input{
                width: px2Rem(229px);
                height: px2Rem(41px);
                background: #F1F5FC;
                border: none;
                border-radius: 5px;
                text-indent: px2Rem(48px);
                font-size: px2Rem(20px);
                &::placeholder{
                    color: #C1C1C1;
                    font-weight: bold;
                }
            }
        }
    }
    .button{
        margin-top: px2Rem(20px);
        display: flex;
        .button-items{
            width: px2Rem(161px);
            height: px2Rem(56px);
            border-top-right-radius: 10px;
            background: #F1F5FC;
            display: flex;
            align-items: center;
            justify-content: space-around;
            cursor: pointer;
            margin-right: px2Rem(10px);
            transition: all .3s;
            * {
                transition: all .3s;
            }
            span{
                font-size: px2Rem(20px);
                color: #818385;
                font-weight: bold;
            }
            div{
                min-width: px2Rem(30px);
                padding: 0 px2Rem(10px);
                background: #4B8AFC;
                border-radius: px2Rem(16px);
                text-align: center;
                color: #fff;
                font-weight: bold;
            }
        }
        .action{
            background: #4C8BFD;
            span{
                color: #fff;
            }
            div{
                background: #fff;
                color: #4C8BFD;
            }
        }
    }
    .table{
        background: #999;
        height: 300px;
        .header{
            height: px2Rem(53px);
            background: #F8FAFA;
            border: 1px solid #EBEBEB;
            padding: 0 35px;
            box-sizing: border-box;
        }
    }
</style>
