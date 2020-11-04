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
<!--        <div class="table">-->
<!--            <Header-->
<!--                :data="['名称代码','最新价','涨跌幅','监听买入价','监听卖出价','监听数量','盈亏金额','市值','可用股数','成交量','运行天数']"-->
<!--                @changeType="changeType"-->
<!--            />-->
<!--            <div class="table-content">-->
<!--                <div class="items">-->
<!--                    <div>-->
<!--                        <p class="ellipsis">美联转债</p>-->
<!--                        <p class="ellipsis">123023.SZ</p>-->
<!--                        <div>35</div>-->
<!--                    </div>-->
<!--                    <div class="ellipsis">103.530</div>-->
<!--                    <div>-3.45%</div>-->
<!--                    <div>-->
<!--                        <p class="ellipsis">101.3</p>-->
<!--                        <p>拐点 : 0.2%</p>-->
<!--                    </div>-->
<!--                    <div>-->
<!--                        <p class="ellipsis">105.3</p>-->
<!--                        <p>拐点 : 无</p>-->
<!--                    </div>-->
<!--                    <div>-->
<!--                        <p class="ellipsis">买入: <span>30</span></p>-->
<!--                        <p class="ellipsis">卖出: <span>10</span></p>-->
<!--                    </div>-->
<!--                    <div>-->
<!--                        <p class="ellipsis">-20394</p>-->
<!--                        <p>盈亏幅度 :<span>-3.52%</span></p>-->
<!--                    </div>-->
<!--                    <div class="ellipsis">104095.33</div>-->
<!--                    <div>-->
<!--                        <p class="ellipsis">300股</p>-->
<!--                        <p class="ellipsis">持仓股数 : 400股</p>-->
<!--                    </div>-->
<!--                    <div>-->
<!--                        <p class="ellipsis">3000万</p>-->
<!--                        <p class="ellipsis">剩余库存 : 848</p>-->
<!--                    </div>-->
<!--                    <div>-->
<!--                        <p class="ellipsis">38天</p>-->
<!--                        <p>Date : 2020.8.23 </p>-->
<!--                    </div>-->
<!--                    <div>删除</div>-->
<!--                    <div>修改</div>-->
<!--                    <div>手动</div>-->
<!--                    <div>-->
<!--                        <div>-->
<!--                            <img src="../assets/up.png"/>-->
<!--                            <div>百分比%</div>-->
<!--                        </div>-->
<!--                        <div>-->
<!--                            <img src="../assets/down.png"/>-->
<!--                            <div>百分比%</div>-->
<!--                        </div>-->
<!--                    </div>-->
<!--                </div>-->
<!--            </div>-->
<!--        </div>-->
        <div class="tb">
<!--            <div class="header">-->
<!--                <div v-for="(item,index) in ['名称代码','最新价','涨跌幅','监听买入价','监听卖出价','监听数量','盈亏金额','市值','可用股数','成交量','运行天数']">{{item}}</div>-->
<!--            </div>-->
            <Header
                :data="['名称代码','最新价','涨跌幅','监听买入价','监听卖出价','监听数量','盈亏金额','市值','可用股数','成交量','运行天数']"
                @changeType="changeType"
            />
            <div class="table-content">
                <div class="items">
                    <div>
                        <p class="ellipsis">美联转债</p>
                        <p class="ellipsis">123023.SZ</p>
                        <div>35</div>
                    </div>
                    <div><span class="ellipsis">103.530</span></div>
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
                            <p>Date : 2020.8.23 </p>
                        </div>
                        <div>
                            <div>删除</div>
                            <div @click="Popindex = 0">修改</div>
                            <div @click="showBigPop = true">手动</div>
                            <div>
                                <div>
                                    <img src="../assets/up.png"/>
                                    <div>百分比%</div>
                                </div>
                                <div>
                                    <img src="../assets/down.png"/>
                                    <div>百分比%</div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <Pop v-show="Popindex === 0" @hiddenPop="Popindex = null"/>
                </div>
            </div>
        </div>
        <BigPop v-if="showBigPop" @hiddenPop="showBigPop = false" key="BigPop"/>
    </div>
</template>

<script>
    import Header from '../components/Header'
    import BigPop from '../components/BigPop'
    import Pop from '../components/Pop'
    export default {
        name: 'MyTask',
        data() {
            return {
                selectIndex: 0,
                showBigPop: false,
                Popindex: null
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
        border: 1px solid #000;
        .table-content{
            padding: 0 px2Rem(15px);
            box-sizing: border-box;
            .items{
                display: flex;
                align-items: center;
                height: px2Rem(80px);
                &>div{
                    position: relative;
                    &:first-child{
                        width: px2Rem(130px);
                        text-align: center;
                        margin-right: px2Rem(10px);
                        p:first-child{
                            font-size: px2Rem(22px);
                            color: #164D9D;
                            font-weight: bold;
                        }
                        p:nth-child(2) {
                            font-size: px2Rem(16px);
                            color: #A2A2A2;
                            font-weight: bold;
                        }
                        div{
                            min-width: px2Rem(15px);
                            padding: 0 px2Rem(5px);
                            border-radius: 12px;
                            background: #FF4050;
                            height: px2Rem(20px);
                            position: absolute;
                            color: #fff;
                            font-size: px2Rem(10px);
                            line-height: 20px;
                            text-align: center;
                            right: px2Rem(0px);
                            top: px2Rem(-10px);
                        }
                    }
                    &:nth-child(2) {
                        font-size: px2Rem(25px);
                        color: #FF4050;
                        font-weight: bold;
                        width: px2Rem(130px);
                        text-align: left;
                    }
                    &:nth-child(3) {
                        font-size: px2Rem(25px);
                        color: #47B133;
                        font-weight: bold;
                        width: px2Rem(135px);
                        text-align: left;
                    }
                    &:nth-child(4),&:nth-child(5) {
                        width: px2Rem(125px);
                        text-align: left;
                        p:first-child{
                            font-weight: bold;
                            color: #3C3C3C;
                            font-size: px2Rem(21px);
                        }
                        p:last-child{
                            color: #A2A2A2;
                            font-size: px2Rem(13px);
                            font-weight: bold;
                            line-height: px2Rem(10px);
                        }
                    }
                    &:nth-child(6) {
                        font-size: px2Rem(16px);
                        color: #A2A2A2;
                        font-weight: bold;
                        width: px2Rem(100px);
                        text-align: left;
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
                        width: px2Rem(150px);
                        text-align: left;
                        p:first-child{
                            font-size: px2Rem(25px);
                            color: #47B133;
                            font-weight: bold;
                        }
                        p:last-child{
                            font-size: px2Rem(13px);
                            color: #A2A2A2;
                            font-weight: bold;
                            line-height: px2Rem(10px);
                            span{
                                color: #47B133;
                            }
                        }
                    }
                    &:nth-child(8) {
                        font-size: px2Rem(19px);
                        color: #FF4050;
                        font-weight: bold;
                    }
                    &:nth-child(9),&:nth-child(10),&:nth-child(11) {
                        p:first-child{
                            font-weight: bold;
                            font-size: px2Rem(19px);
                            color: #000;
                        }
                        p:last-child{
                            line-height: px2Rem(10px);
                            font-size: px2Rem(13px);
                            font-weight: bold;
                            color: #A2A2A2;
                        }
                    }
                    &:nth-child(12),&:nth-child(13),&:nth-child(14) {
                        font-size: px2Rem(19px);
                        color: #4879FF;
                        font-weight: 300;
                        cursor: pointer;
                    }
                    &:nth-child(15){
                        &>div{
                            display: flex;
                            margin-bottom: px2Rem(5px);
                            img{
                                width: px2Rem(15px);
                                margin-right: px2Rem(9px);
                            }
                            div{
                                width: 50px;
                                height: px2Rem(21px);
                                background: #FFFFFF;
                                border: 1px solid #EDEDED;
                                box-shadow: 0px 3px 6px rgba(188, 188, 188, 0.16);
                                opacity: 1;
                                border-radius: 5px;
                                color: #BABABA;
                                font-size: 6px;
                                text-align: center;
                                line-height: px2Rem(21px);
                            }
                        }
                    }
                }
            }
        }
    }
    .tb{
        .table-content{
            /*padding: 0 px2Rem(15px);*/
            box-sizing: border-box;
            .items{
                display: flex;
                align-items: center;
                height: px2Rem(80px);
                position: relative;
                &>div{
                    position: relative;
                    &:first-child{
                        p:first-child{
                            font-size: px2Rem(22px);
                            color: #164D9D;
                            font-weight: bold;
                        }
                        p:nth-child(2) {
                            font-size: px2Rem(16px);
                            color: #A2A2A2;
                            font-weight: bold;
                        }
                        div{
                            min-width: px2Rem(15px);
                            padding: 0 px2Rem(5px);
                            border-radius: 12px;
                            background: #FF4050;
                            height: px2Rem(20px);
                            position: absolute;
                            color: #fff;
                            font-size: px2Rem(10px);
                            line-height: 20px;
                            text-align: center;
                            right: px2Rem(-15px);
                            top: px2Rem(2px);
                        }
                    }
                    &:nth-child(2) {
                        font-size: px2Rem(25px);
                        color: #FF4050;
                        font-weight: bold;
                    }
                    &:nth-child(3) {
                        font-size: px2Rem(25px);
                        color: #47B133;
                        font-weight: bold;
                    }
                    &:nth-child(4),&:nth-child(5) {
                        p:first-child{
                            font-weight: bold;
                            color: #3C3C3C;
                            font-size: px2Rem(21px);
                        }
                        p:last-child{
                            color: #A2A2A2;
                            font-size: px2Rem(13px);
                            font-weight: bold;
                            line-height: px2Rem(10px);
                        }
                    }
                    &:nth-child(6) {
                        font-size: px2Rem(16px);
                        color: #A2A2A2;
                        font-weight: bold;
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
                        p:first-child{
                            font-size: px2Rem(25px);
                            color: #47B133;
                            font-weight: bold;
                        }
                        p:last-child{
                            font-size: px2Rem(13px);
                            color: #A2A2A2;
                            font-weight: bold;
                            /*line-height: px2Rem(10px);*/
                            span{
                                color: #47B133;
                            }
                        }
                    }
                    &:nth-child(8) {
                        font-size: px2Rem(19px);
                        color: #FF4050;
                        font-weight: bold;
                    }
                    &:nth-child(9),&:nth-child(10),&:nth-child(11)>div:first-child {
                        p:first-child{
                            font-weight: bold;
                            font-size: px2Rem(19px);
                            color: #000;
                        }
                        p:last-child{
                            /*line-height: px2Rem(20px);*/
                            position: relative;
                            font-size: px2Rem(13px);
                            font-weight: bold;
                            color: #A2A2A2;
                        }
                    }
                    &:nth-child(11){
                        display: flex;
                        flex-direction: row;
                        justify-content: flex-start;
                        align-items: center;
                        &>div:last-child{
                            flex: 1;
                            display: flex;
                            align-items: center;
                            &>div{
                                font-size: px2Rem(19px);
                                color: #4879FF;
                                font-weight: 300;
                                cursor: pointer;
                            }
                            &>div:last-child{
                                &>div{
                                    display: flex;
                                    margin-bottom: px2Rem(5px);
                                    img{
                                        width: px2Rem(15px);
                                        margin-right: px2Rem(9px);
                                    }
                                    &:last-child img {
                                        transform: rotate(180deg);
                                    }
                                    div{
                                        width: 50px;
                                        height: px2Rem(21px);
                                        background: #FFFFFF;
                                        border: 1px solid #EDEDED;
                                        box-shadow: 0px 3px 6px rgba(188, 188, 188, 0.16);
                                        opacity: 1;
                                        border-radius: 5px;
                                        color: #BABABA;
                                        font-size: 6px;
                                        text-align: center;
                                        line-height: px2Rem(21px);
                                    }
                                }
                            }
                        }
                    }
                    /*&:nth-child(12),&:nth-child(13),&:nth-child(14) {*/
                    /*    font-size: px2Rem(19px);*/
                    /*    color: #4879FF;*/
                    /*    font-weight: 300;*/
                    /*    cursor: pointer;*/
                    /*}*/
                    /*&:last-child{*/
                    /*    &>div{*/
                    /*        display: flex;*/
                    /*        margin-bottom: px2Rem(5px);*/
                    /*        img{*/
                    /*            width: px2Rem(15px);*/
                    /*            margin-right: px2Rem(9px);*/
                    /*        }*/
                    /*        div{*/
                    /*            width: 50px;*/
                    /*            height: px2Rem(21px);*/
                    /*            background: #FFFFFF;*/
                    /*            border: 1px solid #EDEDED;*/
                    /*            box-shadow: 0px 3px 6px rgba(188, 188, 188, 0.16);*/
                    /*            opacity: 1;*/
                    /*            border-radius: 5px;*/
                    /*            color: #BABABA;*/
                    /*            font-size: 6px;*/
                    /*            text-align: center;*/
                    /*            line-height: px2Rem(21px);*/
                    /*        }*/
                    /*    }*/
                    /*}*/
                }
            }
        }
        .items>div{
            overflow: hidden;
            color: #000;
            flex: .4;
            display: flex;
            justify-content: center;
            flex-direction: column;
            text-align: left;
            /*border: 1px solid #000;*/
            height: 100%;
            &:first-child{
                cursor: pointer;
                text-align: right;
                flex: .45;
                /*overflow: visible;*/
            }
            &:nth-child(2) {
                text-align: left;
                flex: .6;
                text-indent: px2Rem(60px);
            }
            &:nth-child(3) {
                text-align: left;
            }
            &:nth-child(4) {
                text-align: left;
            }
            &:nth-child(5) {
                text-align: left;
            }
            &:nth-child(6) {
                text-align: left;
            }
            &:nth-child(7) {
                text-align: left;
            }
            &:nth-child(15){
                flex: 1;
            }

        }
    }
</style>
