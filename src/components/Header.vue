<template>
    <div class="header">
        <div v-for="(item,index) in data" @click="index === 0 ? _set() : ''">
            {{item}}
            <div
                :class="['triangle', type === 'down' ? 'down-triangle' : '']"
                v-show="index === 0"
            >
                <div class="up"></div>
                <div class="down"></div>
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
                type: 'up'
            }
        },
        methods: {
            _set() {
                this.type = this.type === 'up' ? 'down' : 'up'
                this.$emit('changeType', this.type)
            }
        }
    }
</script>

<style scoped lang="scss">
    .header{
        width: 100%;
        height: px2Rem(53px);
        background: #F8FAFA;
        border: 1px solid #EBEBEB;
        /*padding: 0 35px;*/
        box-sizing: border-box;
        display: flex;
        align-items: center;
        &>div{
            position: relative;
            color: #808080;
            font-size: px2Rem(18px);
            font-weight: bold;
            .triangle{
                position: absolute;
                right: px2Rem(40px);
                top: px2Rem(20px);
                .up{
                    width: 0;
                    height: 0;
                    border-left: px2Rem(5px) solid transparent;
                    border-right: px2Rem(5px) solid transparent;
                    border-bottom: px2Rem(6px) solid #808080;
                }
                .down{
                    width: 0;
                    height: 0;
                    border-left: px2Rem(5px) solid transparent;
                    border-right: px2Rem(5px) solid transparent;
                    border-top: px2Rem(6px) solid #C7C7C7;
                    margin-top: px2Rem(2px);
                }
            }
            .down-triangle{
                .up {
                    border-bottom: px2Rem(6px) solid #C7C7C7;
                }
                .down{
                    border-top: px2Rem(6px) solid #808080;
                }
            }
            overflow: hidden;
            flex: .4;
            line-height: px2Rem(53px);
            text-align: left;
            height: 100%;
            &:first-child{
                cursor: pointer;
                text-align: center;
                flex: .65;
            }
            &:nth-child(2) {
                text-align: left;
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
            &:last-child{
                flex: 1;
            }
        }
    }
</style>
