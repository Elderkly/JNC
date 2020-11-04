<template>
    <div class="PoP">
        <div class="header">
            <div>
                <span>证劵代码</span>
                <div>123023</div>
            </div>
            <span>撤销挂单</span>
            <div @click="$emit('hiddenPop')">
                <img src="../assets/close.png">
            </div>
        </div>
        <div class="content">
            <div class="content-top">
                <div>
                    <p>美联转债</p>
                    <p>123023.SZ</p>
                </div>
                <span>103.530</span>
                <span>+13.45%</span>
                <div>
                    <p>300股</p>
                    <p>持仓股数 : 400股</p>
                </div>
            </div>
            <div class="content-middle">
                <Field
                    :text="item.text"
                    :defaultUnit="item.defaultUnit ? item.defaultUnit : '%'"
                    :unit="item.unitArray ? item.unitArray : ['股','元','%']"
                    @select="select => topField[index].unit = select"
                    @changeText="text => topField[index].number = text"
                    @check="check => topField[index].check = check"
                    v-for="(item,index) in topField"
                    :key="index"
                    :type="item.type"
                    :buttonClass="item.buttonClass"
                    inputClass="PopInput"
                    class="PopField"
                />
            </div>
            <div class="content-button">
                <img src="../assets/mbutton1.png"/>
                <img src="../assets/mbutton2.png"/>
                <img src="../assets/mbutton3.png"/>
                <img src="../assets/mbutton4.png"/>
            </div>
            <div class="content-bottom1">
                <Field
                    :text="item.text"
                    :defaultUnit="item.defaultUnit ? item.defaultUnit : '%'"
                    :unit="item.unitArray ? item.unitArray : ['股','元','%']"
                    @select="select => bottomField1[index].unit = select"
                    @changeText="text => bottomField1[index].number = text"
                    @check="check => bottomField1[index].check = check"
                    v-for="(item,index) in bottomField1"
                    :key="index"
                    :type="item.type"
                    :buttonClass="item.buttonClass"
                    inputClass="PopInput"
                    class="PopField"
                />
                <img src="../assets/bbutton1.png">
            </div>
            <div class="content-bottom2">
                <Field
                    :text="item.text"
                    :defaultUnit="item.defaultUnit ? item.defaultUnit : '%'"
                    :unit="item.unitArray ? item.unitArray : ['股','元','%']"
                    @select="select => bottomField2[index].unit = select"
                    @changeText="text => bottomField2[index].number = text"
                    @check="check => bottomField2[index].check = check"
                    v-for="(item,index) in bottomField2"
                    :key="index"
                    :type="item.type"
                    :buttonClass="item.buttonClass"
                    inputClass="PopInput"
                    class="PopField"
                />
                <img src="../assets/bbutton2.png">
            </div>
        </div>
    </div>
</template>

<script>
    import Field from '../components/Field'
    export default {
        name: 'Pop',
        data() {
            return {
                topField: [
                    {
                        text: '回落清仓',
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
                        type: 'Dheckbox',
                        buttonClass:'lastBox',
                    },
                    {
                        text: '回升建仓',
                        number: null,
                        type: 'check',
                        check: false
                    },
                    {
                        text: '买入',
                        number: null,
                        unit: null,
                        defaultUnit: '股',
                        unitArray: ['股','元','全部','1/2','1/3','1/4'],
                        type: 'Dheckbox',
                        buttonClass:'lastBox',
                    },
                ],
                bottomField1: [
                    {
                        text: '',
                        number: null,
                        unit: null,
                        defaultUnit: '股',
                        unitArray: ['股','元','全部','1/2','1/3','1/4'],
                        buttonClass:'lastBox',
                        type: 'Dheckbox'
                    },
                    {
                        text: '优化',
                        number: null,
                        unit: null,
                        type: 'input'
                    },
                ],
                bottomField2: [
                    {
                        text: '',
                        number: null,
                        unit: null,
                        defaultUnit: '股',
                        unitArray: ['股','元','全部','1/2','1/3','1/4'],
                        buttonClass:'lastBox',
                        type: 'Dheckbox'
                    },
                    {
                        text: '优化',
                        number: null,
                        unit: null,
                        type: 'input'
                    },
                ]
            }
        },
        components: {
            Field
        }
    }
</script>

<style lang="scss" scoped>
    .PoP{
        position: absolute!important;
        width: px2Rem(516px);
        height: px2Rem(447px) !important;
        background: #EFEFEF;
        right: px2Rem(84px);
        top: 0;
        border: 1px solid #EFEFEF;
        box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.16);
        opacity: 1;
        border-radius: 20px;
        justify-content: flex-start!important;
        overflow: inherit;
        .header{
            height: px2Rem(64px);
            background: #E9E9E9;
            border-top-left-radius: 20px;
            border-top-right-radius: 20px;
            display: flex;
            align-items: center;
            border-bottom: 1px solid #DDDDDD;
            position: relative;
            span{
                font-size: px2Rem(15px);
                color: #898989;
                margin-right: px2Rem(9px);
                margin-left: px2Rem(30px);
                &:first-child{
                    margin-left: px2Rem(37px);
                }
            }
            &>div:first-child{
                display: flex;
                flex: 1;
                align-items: center;
                div{
                    width: px2Rem(106px);
                    height: px2Rem(27px);
                    background: #FFFFFF;
                    border: 1px solid #E6E6E6;
                    opacity: 1;
                    border-radius: 5px;
                    text-align: center;
                    font-size: px2Rem(16px);
                    color: #000;
                }
            }
            &>span{
                font-size: px2Rem(18px);
                color: #1788FF;
                font-weight: 300;
                margin-right: px2Rem(60px);
                cursor: pointer;
            }
            &>div:last-child{
                position: absolute;
                width: px2Rem(15px);
                height: px2Rem(15px);
                border-radius: 50%;
                background: #ec4e67;
                right: px2Rem(15px);
                top: px2Rem(10px);
                text-align: center;
                line-height: px2Rem(15px);
                cursor: pointer;
                img{
                    width: px2Rem(15px);
                }
            }
        }
        .content{
            padding: px2Rem(35px) px2Rem(25px) 0 px2Rem(32px);
            box-sizing: border-box;
            .content-top{
                display: flex;
                align-items: center;
                justify-content: space-between;
                &>div:first-child{
                    p:first-child{
                        font-weight: bold;
                        font-size: px2Rem(22px);
                        color: #164D9D;
                    }
                    p:last-child{
                        font-weight: bold;
                        font-size: px2Rem(16px);
                        color: #A2A2A2;
                        line-height: px2Rem(20px);
                    }
                }
                &>span:nth-child(2) {
                    font-size: px2Rem(25px);
                    color: #FF4050;
                    font-weight: bold;
                }
                &>span:nth-child(3) {
                    font-size: px2Rem(19px);
                    color: #FF4050;
                    font-weight: bold;
                }
                &>div:last-child{
                    p:first-child{
                        font-weight: bold;
                        font-size: px2Rem(19px);
                        color: #000;
                    }
                    p:last-child{
                        font-weight: bold;
                        font-size: px2Rem(13px);
                        color: #A2A2A2;
                        line-height: px2Rem(15px);
                    }
                }
            }
            .content-middle{
                display: flex;
                flex-wrap: wrap;
                margin-top: px2Rem(21px);
            }
            .content-button{
                margin: px2Rem(25px) px2Rem(5px) px2Rem(30px);
                display: flex;
                align-items: center;
                &>img{
                    width: px2Rem(101px);
                    height: px2Rem(27px);
                    margin-right: px2Rem(10px);
                    cursor: pointer;
                    &:first-child{
                        margin-left: px2Rem(10px);
                    }
                }
            }
            .content-bottom1,.content-bottom2{
                display: flex;
                &>img{
                    width: px2Rem(90px);
                    height: px2Rem(31px);
                    cursor: pointer;
                }
            }
        }
    }
    .PopField:nth-child(2n){
        margin-right: 0;
    }
</style>
