<template>
    <div class="header">
        <div v-for="(item,index) in data" @click="_set(index)">
            <div>
                {{item}}
                <div
                    :style="{opacity: showTriangle && selectIndex === index ? 1 : 0}"
                    :class="['triangle', type === 'down' ? 'down-triangle' : '']"
                >
                    <div class="up"></div>
                    <div class="down"></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Header',
        props: ['data'],
        data() {
            return {
                type: 'up',
                selectIndex: null,
                showTriangle: false
            }
        },
        methods: {
            _set(index) {
                if (this.timeout) {
                    clearTimeout(this.timeout)
                    this.timeout = setTimeout(() => {
                        this.showTriangle = false
                        this.timeout = null
                    },1000)
                } else {
                    this.timeout = setTimeout(() => {
                        this.showTriangle = false
                        this.timeout = null
                    },1000)
                }
                this.showTriangle = true
                if (index === this.selectIndex) {
                    this.type = this.type === 'up' ? 'down' : 'up'
                } else {
                    this.selectIndex = index
                    this.type = 'down'
                }
                this.$emit('changeType', {
                    name: this.data[index],
                    type: this.type
                })
            }
        }
    }
</script>

<style scoped lang="scss">
    @media (min-width: 1920px){
        .header>div:first-child>div{
            margin-left: 34% !important;
        }
    }
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
            position: relative;
            cursor: pointer;
            &:first-child{
                width: 10%;
                &>div{
                    margin-left: 27%;
                }
            }
            &:last-child{
                width: 20%;
            }
            &>div{
                position: absolute;
            }
        }
        .triangle{
            position: absolute;
            right: px2Rem(-10px);
            top: px2Rem(20px);
            opacity: 0;
            transition: all .3s;
            .up{
                width: 0;
                height: 0;
                border-left: px2Rem(3px) solid transparent;
                border-right: px2Rem(3px) solid transparent;
                border-bottom: px2Rem(4px) solid #808080;
            }
            .down{
                width: 0;
                height: 0;
                border-left: px2Rem(3px) solid transparent;
                border-right: px2Rem(3px) solid transparent;
                border-top: px2Rem(4px) solid #C7C7C7;
                margin-top: px2Rem(2px);
            }
        }
        .down-triangle{
            .up {
                border-bottom: px2Rem(4px) solid #C7C7C7;
            }
            .down{
                border-top: px2Rem(4px) solid #808080;
            }
        }
    }
</style>
