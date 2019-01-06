<template>
    <div class="wrapper" id="wrapper">
        <div class="output">
            <span class="num">{{num}}</span>
        </div>
        <div id="input" class="input">
            <div class="line1 line">
                <div class="btn">AC</div>
                <div class="btn">+/-</div>
                <div class="btn">%</div>
                <div class="btn">÷</div>
            </div>
            <div class="line2 line">
                <div class="btn">7</div>
                <div class="btn">8</div>
                <div class="btn">9</div>
                <div class="btn">×</div>
            </div>
            <div class="line3 line">
                <div class="btn">4</div>
                <div class="btn">5</div>
                <div class="btn">6</div>
                <div class="btn">-</div>
            </div>
            <div class="line4 line">
                <div class="btn">1</div>
                <div class="btn">2</div>
                <div class="btn">3</div>
                <div class="btn">+</div>
            </div>
            <div class="line5 line">
                <div class="btn">0</div>
                <div class="btn">.</div>
                <div class="btn">=</div>
            </div>
        </div>

    </div>
</template>

<script>
    import SystemInformation from './LandingPage/SystemInformation'

    export default {
        name: 'landing-page',
        components: {SystemInformation},
        data() {
            return {
                num: 0
            }
        },
        mounted(){
            input.addEventListener('click',function (x) {
                console.log(x.target.innerText)
            })
        },
        methods: {
            open(link) {
                this.$electron.shell.openExternal(link)
            }
        }
    }
</script>

<style lang="scss">
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    .wrapper {
        display: flex;
        flex-direction: column;

        .output {
            height: 64px;
            background-color: #535457;
            color: #fff;
            position: relative;

            .num {
                position: absolute;
                bottom: 0;
                right: 20px;
                font-size: 38px;
            }
        }

        .input {
            .line {
                display: flex;
                width: 100%;
                align-items: center;

                .btn {
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    height: 48px;
                    font-size: 18px;
                    border-top: 1px solid #5B5C60;
                    border-left: 1px solid #5B5C60;
                    width: 25%;
                    color: #fff;
                    background-color: #868789;
                    &:active{
                        background-color: #b0b0b1;
                    }

                    &:last-child {
                        border-right: 1px solid #5B5C60;
                        background-color: #FF9F0A;

                        &:active {
                            background-color: #c47208;
                        }
                    }
                }

            }

            .line1 {
                .btn {
                    background-color: #6C6D6F;

                    &:active {
                        background-color: #868789;
                    }
                }

            }

            .line5 {
                .btn {
                    &:first-child {
                        width: 50%;
                    }

                    border-bottom: 1px solid #303747;
                }
            }
        }
    }

</style>
