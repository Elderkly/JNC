<template>
    <div :class="['field',type === 'check' ? 'check-big-box' : '', type === 'BigDheckbox' ? 'BigDheckbox' : '' ]">
        <div class="checkBox" v-show="type === 'check'" @click="_check">
            <div class="action" v-show="check"></div>
        </div>
        <span>{{text}}</span>
        <input :class="inputClass ? inputClass : '' " v-show="type !== 'BigDheckbox'" type="text" @input="_input" ref="input">
        <span v-show="type === 'check' || type === 'input'">{{defaultUnit}}</span>
        <div :class="['button', buttonClass ? buttonClass : '']" @click="showtag = !showtag" ref="buttonBox" v-show="type !== 'check' && type !== 'input'">
            <span>{{select}}</span>
            <div class="buttonBox">
                <img src="../assets/icon-up.png">
                <img src="../assets/icon-down.png">
            </div>
            <div class="tag" v-show="showtag">
                <div v-for="(item,index) in unit" :class="[select === item ? 'action' : '']" @click.stop="_select(item)">
                    <img src="../assets/success.png" :style="{opacity: select === item ? 1 : 0}">
                    <span>{{item}}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Field',
        props: ['text','defaultUnit','unit','type','buttonClass','inputClass'],
        data() {
            return {
                showtag: false,
                select: this.defaultUnit,
                check: false
            }
        },
        methods: {
            _input() {
                this.$emit('changeText', event.target.value)
            },
            _select(item) {
                this.select = item
                this.showtag = false
                if(this.type === 'Dheckbox' && item !== '股' && item!== '元') {
                    this.$refs.input.value = this.select
                }
                this.$emit('select',this.select)
            },
            setUpShow(e) {
                const _con = this.$refs.buttonBox;   // 设置目标区域
                if (_con !== e.target && !_con.contains(e.target)) {
                    this.showtag = false
                }
            },
            _check() {
                this.check = !this.check
                this.$emit('check',this.check)
            }
        },
        watch: {
            showtag(newValue) {
                if (newValue) {
                    document.body.addEventListener('mouseup',this.setUpShow)
                } else {
                    document.body.removeEventListener('mouseup',this.setUpShow)
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .field{
        display: flex;
        align-items: center;
        margin-right: px2Rem(15px);
        margin-bottom: px2Rem(7px);
        &>span{
            font-size: px2Rem(15px);
            color: #898989;
            margin-right: px2Rem(9px);
        }
        input{
            width: px2Rem(110px);
            height: px2Rem(30px);
            background: #FFFFFF;
            border: 1px solid #E6E6E6;
            border-radius: 5px;
            text-align: center;
            font-size: px2Rem(15px);
            color: #212121;
            margin-right: 5px;
        }
        @media screen and (max-width: 1380px) {
            input{
                width: px2Rem(100px);
            }
        }
        .button{
            width: px2Rem(60px);
            height: px2Rem(30px);
            border-radius: 5px;
            font-size: px2Rem(15px);
            color: #898989;
            background: #FFFFFF;
            border: 1px solid #E6E6E6;
            display: flex;
            align-items: center;
            box-sizing: border-box;
            padding: 0 px2Rem(3px) 0 px2Rem(9px);
            cursor: pointer;
            position: relative;
            span{
                flex: 1;
            }
            .buttonBox{
                width: px2Rem(24px);
                height: px2Rem(24px);
                background: #1788FF;
                border-radius: 5px;
                display: flex;
                flex-direction: column;
                align-items: center;
                position: relative;
                img{
                    width: px2Rem(11px);
                }
            }
        }
        .tag{
            position: absolute;
            right: px2Rem(3px);
            top: px2Rem(3px);
            width: 100%;
            background: #EFEFEF;
            padding: px2Rem(3px);
            display: flex;
            align-items: center;
            flex-direction: column;
            border: 1px solid #E6E6E6;
            box-shadow: 0px 3px 6px rgba(131, 131, 131, 0.16);
            border-radius: 5px;
            z-index: 10;
            div{
                width: 100%;
                background: #EFEFEF;
                display: flex;
                border-radius: px2Rem(4px);
                justify-content: center;
                height: px2Rem(21px);
                img{
                    width: px2Rem(16px);
                    margin: 0 10%;
                }
                span{
                    color: #070707;
                    font-size: px2Rem(12px);
                    text-align: left;
                }
                &:hover{
                    /*background: #459CFF;*/
                    /*span{*/
                    /*    color: #fff;*/
                    /*}*/
                }
            }
            .action{
                background: #459CFF;
                span{
                    color: #fff;
                }
            }
        }
        .checkBox{
            width: px2Rem(17px);
            height: px2Rem(17px);
            background: #FFFFFF;
            border: 1px solid #E0E0E0;
            border-radius: 50%;
            margin-right: px2Rem(7px);
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            .action{
                width: px2Rem(11px);
                height: px2Rem(11px);
                border-radius: 50%;
                background: #1788FF;
            }
        }
    }
    .check-big-box{
        margin-right: px2Rem(9px);
        .button{
            width: px2Rem(75px);
        }
    }
    .BigDheckbox{
        .button{
            text-align: center;
            color: #070707;
        }
        .tag{
            top: px2Rem(25px);
            left: px2Rem(-5px);
        }
    }
</style>
