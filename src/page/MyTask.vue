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
        <div class="fixedHeaderBox">
            <div class="tableBox">
                <div class="table">
                    <Header
                        class="opacityHeader"
                        @changeType="changeType"
                        :data="['名称代码','最新价','涨跌幅','监听买入价','监听卖出价','监听数量','盈亏金额','市值','可用股数','成交量','运行天数','']"
                    />
                    <div class="items" v-for="item in [...new Array(20)]">
                        <div>
                            <div>
                                <span class="ellipsis">美联转债</span>
                                <span class="ellipsis">123023.SZ</span>
                                <div>35</div>
                            </div>
                        </div>
                        <div class="ellipsis">103.530</div>
                        <div>-3.45%</div>
                        <div>
                            <p class="ellipsis">101.3</p>
                            <p>拐点 : 0.2%</p>
                        </div>
                        <div>
                            <p class="ellipsis">105.3</p>
                            <p>拐点 : 无</p>
                        </div>
                        <div>
                            <p class="ellipsis">买入: <span>30</span></p>
                            <p class="ellipsis">卖出: <span>10</span></p>
                        </div>
                        <div>
                            <p class="ellipsis">-20394</p>
                            <p class="ellipsis">盈亏幅度 :<span>-3.52%</span></p>
                        </div>
                        <div class="ellipsis">104095.33</div>
                        <div>
                            <p class="ellipsis">300股</p>
                            <p class="ellipsis">持仓股数 : 400股</p>
                        </div>
                        <div>
                            <p class="ellipsis">3000万</p>
                            <p class="ellipsis">剩余库存 : 848</p>
                        </div>
                        <div>
                            <div>
                                <p class="ellipsis">38天</p>
                                <p class="ellipsis">Date : 2020.8.23 </p>
                            </div>
                        </div>
                        <div>
                            <span>删除</span>
                            <span @click="$emit('ShowBigPop')">修改</span>
                            <span @click="showPop">手动</span>
                            <div>
                                <div>
                                    <img src="../assets/up.png"/>
                                    <input placeholder="百分比%"/>
                                </div>
                                <div>
                                    <img src="../assets/down.png"/>
                                    <input placeholder="百分比%">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="fixedHeader">
                <Header
                    @changeType="changeType"
                    :data="['名称代码','最新价','涨跌幅','监听买入价','监听卖出价','监听数量','盈亏金额','市值','可用股数','成交量','运行天数','']"
                />
            </div>
        </div>
    </div>
</template>

<script>
    import Header from '../components/Header'
    import Pop from '../components/Pop'
    export default {
        name: 'MyTask',
        data() {
            return {
                selectIndex: 0,
                Popindex: null
            }
        },
        methods: {
            changeType(type) {
                console.log('排序变化变更',type)
            },
            showPop() {
                this.$emit('showPop',event.pageY)
            }
        },
        components: {
            Header,
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
            font-weight: 400;
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
                font-size: px2Rem(18px);
                line-height: px2Rem(41px);
                &::placeholder{
                    color: #C1C1C1;
                    font-weight: 400;
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
                font-weight: 400;
            }
            div{
                min-width: px2Rem(30px);
                padding: 0 px2Rem(10px);
                background: #4B8AFC;
                border-radius: px2Rem(16px);
                text-align: center;
                color: #fff;
                font-weight: 400;
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

    /*::-webkit-scrollbar {*/
        /*display: none; !* Chrome Safari *!*/
    /*}*/
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
                font-weight: 400;
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
                &:first-child{
                    position: relative;
                    display: flex;
                    justify-content: center;
                    overflow: inherit;
                    &>div{
                        position: absolute;
                        display: flex;
                        flex-direction: column;
                        line-height: px2Rem(23px);
                        text-align: center;
                        top: px2Rem(15px);
                        max-width: 100%;
                        span:first-child{
                            font-size: px2Rem(20px);
                            color: #164D9D;
                            font-weight: 400;
                        }
                        span:nth-child(2) {
                            font-size: px2Rem(12px);
                            color: rgba(162, 162, 162, 1);
                            font-weight: 400;
                        }
                        div{
                            position: absolute;
                            right: px2Rem(-15px);
                            top: px2Rem(-10px);
                            background: rgba(255, 64, 80, 1);
                            border-radius: px2Rem(12px);
                            padding: 0 px2Rem(5px);
                            font-size: px2Rem(12px);
                            min-width: px2Rem(18px);
                            color: #fff;
                        }
                    }
                }
                &:nth-child(2) {
                    font-size: px2Rem(22px);
                    color: #FF4050;
                    font-weight: 400;
                }
                &:nth-child(3) {
                    font-size: px2Rem(22px);
                    color: #47B133;
                    font-weight: 400;
                }
                &:nth-child(4),&:nth-child(5) {
                    line-height: px2Rem(23px);
                    p{
                        position: relative;
                        top: -7px;
                    }
                    p:first-child{
                        font-weight: 400;
                        color: #3C3C3C;
                        font-size: px2Rem(18px);
                    }
                    p:last-child{
                        color: #A2A2A2;
                        font-size: px2Rem(10px);
                        font-weight: 400;
                    }
                }
                &:nth-child(6) {
                    font-size: px2Rem(16px);
                    color: #A2A2A2;
                    font-weight: 400;
                    line-height: px2Rem(23px);
                    p{
                        position: relative;
                        top: -7px;
                    }
                    p:first-child{
                        span{
                            color: #47B133;
                        }
                    }
                    p:last-child{
                        span{
                            color: #FF4050;
                        }
                    }
                }
                &:nth-child(7) {
                    line-height: px2Rem(23px);
                    p{
                        position: relative;
                        top: -7px;
                    }
                    p:first-child{
                        font-size: px2Rem(22px);
                        color: #47B133;
                        font-weight: 400;
                    }
                    p:last-child{
                        font-size: px2Rem(10px);
                        color: #A2A2A2;
                        font-weight: 400;
                        span{
                            color: #47B133;
                        }
                    }
                }
                &:nth-child(8) {
                    font-size: px2Rem(19px);
                    color: #FF4050;
                    font-weight: 400;
                }
                &:nth-child(9),&:nth-child(10),&:nth-child(11) {
                    line-height: px2Rem(23px);
                    p{
                        position: relative;
                        top: -7px;
                    }
                    p:first-child{
                        font-weight: 400;
                        font-size: px2Rem(19px);
                        color: #000;
                    }
                    p:last-child{
                        font-size: px2Rem(10px);
                        font-weight: 400;
                        color: #A2A2A2;
                    }
                }
                &:nth-child(12){
                    display: flex;
                    font-size: px2Rem(16px);
                    color: #4879FF;
                    font-weight: 300;
                    cursor: pointer;
                    &>span{
                        margin-right: px2Rem(20px);
                        &:nth-child(3){
                            margin-right: px2Rem(30px);
                        }
                    }
                    &>div{
                        &>div{
                            display: flex;
                            margin-bottom: px2Rem(3px);
                            align-items: center;
                            &:first-child{
                                margin-top: px2Rem(3px);
                            }
                        }
                        img{
                            width: px2Rem(15px);
                            height: px2Rem(20px);
                            margin-right: px2Rem(9px);
                        }
                        &>div:last-child img {
                            transform: rotate(180deg);
                        }
                        &>div input{
                            width: 50px;
                            height: px2Rem(21px);
                            background: #FFFFFF;
                            border: 1px solid #EDEDED;
                            box-shadow: 0px 3px 6px rgba(188, 188, 188, 0.16);
                            opacity: 1;
                            border-radius: 5px;
                            color: #BABABA;
                            font-size: px2Rem(10px);
                            text-align: center;
                            line-height: px2Rem(21px);
                        }
                    }
                }
            }
        }
    }
</style>
