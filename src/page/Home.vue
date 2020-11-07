<template>
  <div class="home-box">
      <div class="home-top">
          <div class="headerBox" @click="showVip = !showVip">
              <img src="../assets/user-header.jpg"/>
          </div>
          <div class="vip-box" v-show="showVip">
              <p>会员剩余天数</p>
              <p>128</p>
              <button @click.stop="showShade = !showShade">续费</button>
              <button @click.stop="logout">退出</button>
          </div>
          <div>
              <img src="../assets/icon-red.png"/>
              <div class="right-items">
                  <p>1028488.33</p>
                  <p>我的资产</p>
              </div>
              <div class="right-items">
                  <p>1028488.33</p>
                  <p>我的资产</p>
              </div>
              <div class="right-items">
                  <p>+28488.33</p>
                  <p>总盈亏</p>
              </div>
              <div class="right-items">
                  <p>-88.33</p>
                  <p>当日盈亏</p>
              </div>
          </div>
      </div>
      <div class="home-bottom">
          <div class="home-left">
              <div
                  :class="['left-button', selectIndex === index ? 'action' : '']"
                  v-for="(item, index) in ['设置任务','我的任务','我的持仓','可转债','任务记录']"
                  @click="changeSelectIndex(index)"
              >
                  <div class="icon"></div>
                  <p>{{item}}</p>
              </div>
          </div>
          <div class="home-right">
              <SetupTask v-if="selectIndex === 0"/>
              <MyTask v-else-if="selectIndex === 1" @ShowBigPop="showBigPop = true" @showPop="showPop"/>
              <MyPosition v-else-if="selectIndex === 2"/>
              <Bond v-else-if="selectIndex === 3"/>
              <TaskRecord v-else/>
          </div>
      </div>
      <BigPop v-if="showBigPop" @hiddenPop="showBigPop = false" key="BigPop"/>
      <Pop v-if="PopTop" :style="{top: PopTop + 'px'}" @hiddenPop="PopTop = null" key="Pop"/>
      <div class="plat" ref="plat"></div>
<!--      <button @click="logout">logout</button>-->
      <div class="showShade" v-show="showShade" @click="showShade = false">
          <div>
              <img src="../assets/QRCode.png"/>
              <p>2999元/年</p>
          </div>
      </div>
  </div>
</template>

<script>
    import SetupTask from './SetupTask'
    import MyTask from './MyTask'
    import MyPosition from './MyPosition'
    import Bond from './Bond'
    import TaskRecord from './TaskRecord'
    import BigPop from '../components/BigPop'
    import Pop from '../components/Pop'
    export default {
        name: 'Home',
        data() {
            return {
                selectIndex: 1,
                showBigPop: false,
                PopTop: null,
                showVip: false,
                showShade: false
            }
        },
        methods: {
            logout() {
                localStorage.removeItem('USERINFO')
                this.$router.push('login')
            },
            changeSelectIndex(index) {
                if (index === 0) {
                    this.showBigPop = true
                } else {
                    this.selectIndex = index
                }
            },
            showPop(Y) {
                if (this.$refs.plat.clientHeight+Y > document.body.clientHeight) {
                    this.PopTop = document.body.clientHeight - this.$refs.plat.clientHeight - 10
                } else {
                    this.PopTop = Y
                }
            }
        },
        components: {
            SetupTask,
            MyTask,
            MyPosition,
            Bond,
            TaskRecord,
            BigPop,
            Pop
        }
    }
</script>

<style lang="scss" scoped>
    .home-box{
        height: 100vh;
        overflow: hidden;
        background: rgba(246, 246, 250, 1);
        padding: px2Rem(15px);
        box-sizing: border-box;
        .home-top{
            display: flex;
            align-items: center;
            .headerBox{
                width: px2Rem(75px);
                height: px2Rem(75px);
                border-radius: 5px;
                margin-right: px2Rem(15px);
                background: #fff;
                box-shadow: 0px 3px 6px rgba(213, 213, 213, 0.16);
                overflow: hidden;
                cursor: pointer;
                &>img{
                    width: px2Rem(75px);
                    height: px2Rem(75px);
                }
            }
            &>div:last-child{
                flex: 1;
                background: #fff;
                display: flex;
                height: px2Rem(75px);
                border-radius: 5px;
                align-items: center;
                box-shadow: 0px 3px 6px rgba(213, 213, 213, 0.16);
                &>img{
                    width: px2Rem(48px);
                    height: px2Rem(45px);
                    margin-right: px2Rem(15px);
                    margin-left: px2Rem(48px);
                }
                .right-items{
                    margin-right: px2Rem(50px);
                    p:first-child{
                        font-size: px2Rem(25px);
                        font-weight: 400;
                        color: rgba(255, 100, 113, 1);
                        line-height: px2Rem(30px);
                    }
                    p:last-child{
                        font-size: px2Rem(10px);
                        color: rgba(208, 208, 208, 1);
                        line-height: px2Rem(8px);
                    }
                    &:last-child p:first-child{
                        color: rgba(10, 187, 7, 1);
                    }
                }
            }
        }
        .vip-box{
            position: absolute;
            width: px2Rem(120px);
            height: px2Rem(93px);
            border-radius: 10px;
            border: 1px solid rgba(239, 239, 239, 1);
            background: #fff;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px 0;
            left: 0;
            top: px2Rem(80px);
            p:first-child{
                font-size: px2Rem(9px);
                color: rgba(183, 183, 183, 1);
            }
            P:nth-child(2) {
                font-size: px2Rem(16px);
                color: rgba(255, 107, 58, 1);
                margin: 3px 0;
            }
            button {
                border: none;
                width: px2Rem(60px);
                height: px2Rem(20px);
                background: #ee6c5b;
                color: #fff;
                font-size: 6px;
                text-align: center;
                line-height: px2Rem(20px);
                border-radius: 2px;
            }
            button:last-child{
                margin-top: 5px;
                background: #a5a5a5;
            }
        }
        .home-bottom{
            display: flex;
            margin-top: px2Rem(15px);
            /*height: 83vh;*/
            min-height: 450px;
            overflow: hidden;
            .home-left{
                width: px2Rem(75px);
                background: rgba(0, 0, 0, .82);
                border-radius: 5px;
                display: flex;
                flex-direction: column;
                align-items: center;
                padding: px2Rem(21px) 0;
                box-sizing: border-box;
                margin-right: px2Rem(15px);
                box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.16);
                font-weight: 300;
                .left-button{
                    display: flex;
                    flex-direction: column;
                    align-items: center;
                    margin-bottom: px2Rem(25px);
                    cursor: pointer;
                    div{
                        /*background-image: url("../assets/icon.png");*/
                        background-size: 100% 100%;
                        margin-bottom: px2Rem(7px);
                        transition: all .3s;
                    }
                    p{
                        color: rgba(188, 188, 188, 1);
                        font-size: px2Rem(10px);
                        transition: all .3s;
                    }
                    &:first-child div{
                        width: px2Rem(41px);
                        height: px2Rem(41px);
                        background-image: url("../assets/button1.png");
                        &:hover{
                            background-image: url("../assets/button1-in.png");
                        }
                    }
                    &:nth-child(2) div{
                        width: px2Rem(38px);
                        height: px2Rem(39px);
                        background-image: url("../assets/button2.png");
                        &:hover{
                            background-image: url("../assets/button2-in.png");
                        }
                    }
                    &:nth-child(3) div{
                        width: px2Rem(33px);
                        height: px2Rem(39px);
                        background-image: url("../assets/button3.png");
                        &:hover{
                            background-image: url("../assets/button3-in.png");
                        }
                    }
                    &:nth-child(4) div{
                        width: px2Rem(33px);
                        height: px2Rem(46px);
                        background-image: url("../assets/button4.png");
                        &:hover{
                            background-image: url("../assets/button4-in.png");
                        }
                    }
                    &:nth-child(5) div{
                        width: px2Rem(29px);
                        height: px2Rem(35px);
                        background-image: url("../assets/button5.png");
                        &:hover{
                            background-image: url("../assets/button5-in.png");
                        }
                    }
                }
                .action{
                    p{
                        color: rgba(10, 187, 7, 1);
                    }
                    &:first-child div {
                        background-image: url("../assets/button1-in.png");
                    }
                    &:nth-child(2) div {
                        background-image: url("../assets/button2-in.png");
                    }
                    &:nth-child(3) div {
                        background-image: url("../assets/button3-in.png");
                    }
                    &:nth-child(4) div {
                        background-image: url("../assets/button4-in.png");
                    }
                    &:nth-child(5) div {
                        background-image: url("../assets/button5-in.png");
                    }
                }
            }
            .home-right{
                flex: 1;
                background: #fff;
                border-radius: 5px;
                padding: px2Rem(25px) px2Rem(35px);
                box-sizing: border-box;
                box-shadow: 0px 3px 6px rgba(193, 193, 193, 0.16);
            }
        }
    }
    .plat{
        height: px2Rem(447px);
        position: absolute;
        top: 0;
        left: 0;
        z-index: -1;
    }
    .showShade{
        position: absolute;
        width: 100%;
        height: 100vh;
        background: rgba(0,0,0,.55);
        top: 0;
        left: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        &>div{
            width: px2Rem(522px);
            height: px2Rem(425px);
            background: rgba(0,0,0,.92);
            border-radius: 22px;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            img{
                width: px2Rem(220px);
            }
            p{
                margin-top: px2Rem(31px);
                font-size: px2Rem(40px);
                color: rgba(255, 94, 89, 1);
            }
        }
    }
</style>
