<template>
    <div class="my-position">
        <div class="select">
            <span>可转债</span>
            <div>
                <img src="../assets/search.png">
                <input type="text" placeholder="搜索">
            </div>
        </div>
        <div class="button">
            <div
                :class="['button-items',selectIndex === index ? 'action' : '']"
                v-for="(item, index) in [{text:'交易记录',number: 135},{text:'历史记录',number: 101}]"
                @click="selectIndex = index"
            >
                <span>{{item.text}}</span>
                <div>{{item.number}}</div>
            </div>
        </div>
        <div class="tableBox">
            <div class="table">
                <Header
                    @changeType="changeType"
                    :data="['证劵代码','证劵名称','最新价','涨跌幅','股票余额','可用余额','冻结数量','盈亏金额','市值','盈亏比例','成本价','持仓天数']"
                />
                <div class="items" v-for="item in [...new Array(5)]">
                    <div class="ellipsis">123023</div>
                    <div class="ellipsis">美联转债</div>
                    <div>103.530</div>
                    <div>-3.45%</div>
                    <div>293004</div>
                    <div>293849</div>
                    <div>300</div>
                    <div>-20394</div>
                    <div>10405.33</div>
                    <div>-3.5%</div>
                    <div>104</div>
                    <div>38天</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Header from '../components/Header'
    import BigPop from '../components/BigPop'
    import Pop from '../components/Pop'
    export default {
        name: 'Bond',
        data() {
            return {
                selectIndex: 0,
            }
        },
        methods: {
            changeType(type) {
                console.log('排序变化变更',type)
            }
        },
        components: {
            Header,
            BigPop,
            Pop
        }
    }
</script>

<style lang="scss" scoped>
    .select{
        display: flex;
        align-items: center;
        span{
            font-size: px2Rem(18px);
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
                font-size: px2Rem(18px);
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
    .tableBox{
        border: 1px solid #EBEBEB;
        height: 60vh;
    }
    ::-webkit-scrollbar {
        display: none; /* Chrome Safari */
    }
    .table{
        display: table;
        width: 100%;
        table-layout: fixed;
        .header{
            display: table-row;
            height: px2Rem(53px);
            background: #F8FAFA;
            border: 1px solid #EBEBEB;
            line-height: px2Rem(53px);
            &>div{
                display: table-cell;
                color: #808080;
                font-size: px2Rem(16px);
                font-weight: bold;
                text-align: left;
                &:first-child{
                    text-align: center;
                }
                &:last-child{
                    width: 20%;
                }
            }
        }
        .items{
            display: table-row;
            height: px2Rem(60px);
            line-height: px2Rem(60px);
            &:hover{
                background: rgba(7, 193, 116, .1) !important;
            }
            &:nth-child(2n + 1) {
                background: rgba(181, 181, 181, .1);
            }
            &>div{
                display: table-cell;
                overflow: hidden;
                &:nth-child(1) {
                    text-align: center;
                    font-size: px2Rem(18px);
                    color: #164D9D;
                    font-weight: bold;
                }
                &:nth-child(2) {
                    font-size: px2Rem(18px);
                    color: #164D9D;
                    font-weight: bold;
                }
                &:nth-child(3),&:nth-child(9) {
                    font-size: px2Rem(20px);
                    color: #FF4050;
                    font-weight: bold;
                }
                &:nth-child(4),&:nth-child(8),&:nth-child(10) {
                    font-size: px2Rem(20px);
                    color: #47B133;
                    font-weight: bold;
                }
                &:nth-child(5),&:nth-child(6),&:nth-child(7) {
                    font-size: px2Rem(17px);
                    color: #3C3C3C;
                    font-weight: bold;
                }
                &:nth-child(11),&:nth-child(12) {
                    font-size: px2Rem(16px);
                    color: #000;
                    font-weight: bold;
                }
            }
        }
    }
</style>
