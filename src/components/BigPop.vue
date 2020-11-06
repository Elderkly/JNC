<template>
    <div class="big-pop">
        <div class="big-pop-content" ref="pop">
            <div class="header">
                <span>证劵代码</span>
                <input type="text"  v-model="Code">
                <span>基准价格</span>
                <input type="text" v-model="Money">
            </div>
            <div class="content">
                <div class="top-field">
                    <Field
                        :text="item.text"
                        :defaultUnit="item.defaultUnit ? item.defaultUnit : '%'"
                        :unit="item.unitArray ? item.unitArray : ['股','元','%']"
                        @select="select => Field[index].unit = select"
                        @changeText="text => Field[index].number = text"
                        @check="check => Field[index].check = check"
                        v-for="(item,index) in Field"
                        :key="index"
                        :type="item.type"
                        :buttonClass="item.buttonClass"
                        class="BigPopField"
                    />
                </div>
                <div class="buttonBox">
                    <div @click="submit">确定</div>
                    <div @click="$emit('hiddenPop')">取消</div>
                </div>
            </div>
            <div
                class="moveView"
                @mousedown="_mousedown"
            ></div>
        </div>
    </div>
</template>

<script>
    import Field from '../components/Field'
    import TouchMove from '../touchMove'
    export default {
        name: 'BigProp',
        components: {
            Field
        },
        data() {
            return {
                Code: null,
                Money: 105,
                Field: [
                    {
                        text: '买入数量',
                        number: null,
                        unit: null
                    },
                    {
                        text: '下跌幅度',
                        number: null,
                        unit: null
                    },
                    {
                        text: '买入拐点',
                        number: null,
                        unit: null
                    },
                    {
                        text: '卖出数量',
                        number: null,
                        unit: null
                    },
                    {
                        text: '上涨幅度',
                        number: null,
                        unit: null
                    },
                    {
                        text: '卖出拐点',
                        number: null,
                        unit: null
                    },
                    {
                        text: '区间高点',
                        number: null,
                        unit: null
                    },
                    {
                        text: '突然回落',
                        number: null,
                        type: 'check',
                        check: false
                    },
                    {
                        text: '清仓',
                        number: null,
                        unit: null,
                        defaultUnit: '股',
                        unitArray: ['股','元','全部','1/2','1/3','1/4'],
                        buttonClass:'lastBox',
                        type: 'Dheckbox'
                    },
                    {
                        text: '区间低点',
                        number: null,
                        unit: null
                    },
                    {
                        text: '突然回升',
                        number: null,
                        type: 'check',
                        check: false
                    },
                    {
                        text: '清仓',
                        number: null,
                        unit: null,
                        defaultUnit: '股',
                        unitArray: ['股','元','全部','1/2','1/3','1/4'],
                        buttonClass:'lastBox',
                        type: 'Dheckbox'
                    },
                    {
                        text: '交易方案',
                        unit: null,
                        defaultUnit: '无限网络',
                        unitArray: ['无限网络','倒金字塔网络'],
                        buttonClass:'lastBigBox',
                        type: 'BigDheckbox'
                    },
                ],
                startX: null,
                startY: null,
                oldX: 0,
                oldY: 0,
                max: []
            }
        },
        methods: {
            submit() {
                console.log(this.Field)
                this.$emit('hiddenPop')
            },
            _mousedown(event) {
                TouchMove(event, this.$refs.pop)
            }
        }
    }
</script>

<style lang="scss" scoped>
    .big-pop{
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        background: rgba(0,0,0,.65);
        /*display: flex;*/
        /*align-items: center;*/
        /*justify-content: center;*/
        user-select:none;
        .big-pop-content{
            width: px2Rem(854px);
            height: px2Rem(562px);
            background: #EFEFEF;
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            position: absolute;
            top: calc(50% - 562px / 2);
            left: calc(50% - 854px / 2);
            .header{
                height: px2Rem(73px);
                background: #E9E9E9;
                border-top-left-radius: 20px;
                border-top-right-radius: 20px;
                display: flex;
                align-items: center;
                border-bottom: 1px solid #DDDDDD;
                span{
                    font-size: px2Rem(15px);
                    color: #898989;
                    margin-right: px2Rem(9px);
                    margin-left: px2Rem(30px);
                    &:first-child{
                        margin-left: px2Rem(37px);
                    }
                }
            }
            .content{
                flex: 1;
                box-sizing: border-box;
                padding: px2Rem(15px) px2Rem(30px) px2Rem(45px) px2Rem(37px);
                .top-field{
                    display: flex;
                    flex-wrap: wrap;
                }
            }
            .moveView{
                position: absolute;
                width: 100%;
                height: px2Rem(50px);
                top: 0;
                cursor: pointer;
            }
        }
        input{
            width: px2Rem(120px);
            height: px2Rem(30px);
            background: #FFFFFF;
            border: 1px solid #E6E6E6;
            border-radius: 5px;
            text-align: center;
            font-size: px2Rem(15px);
            color: #212121;
        }
        .buttonBox{
            margin-top: px2Rem(180px);
            display: flex;
            justify-content: flex-end;
            &>div{
                font-size: px2Rem(15px);
                color: #fff;
                width: px2Rem(101px);
                height: px2Rem(27px);
                cursor: pointer;
                border-radius: 3px;
                text-align: center;
                line-height: px2Rem(27px);
                &:first-child{
                    background: #1788FF;
                    margin-right: px2Rem(26px);
                }
                &:last-child{
                    background: #bfbfbf;
                }
            }
        }
    }
    .BigPopField:nth-child(3n) {
        margin-right: 0;
    }
</style>
