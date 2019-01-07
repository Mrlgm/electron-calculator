<template>
    <div class="wrapper" id="wrapper">
        <div class="output">
            <span class="num">{{output}}</span>
        </div>
        <div id="input" class="input">
            <div class="line1 line">
                <div class="btn" @click="clean">{{isAC}}</div>
                <div class="btn" @click="negate()">+/-</div>
                <div class="btn" @click="mod()">%</div>
                <div class="btn" @click="divide()">÷</div>
            </div>
            <div class="line2 line">
                <div class="btn">7</div>
                <div class="btn">8</div>
                <div class="btn">9</div>
                <div class="btn" @click="multiply()">×</div>
            </div>
            <div class="line3 line">
                <div class="btn">4</div>
                <div class="btn">5</div>
                <div class="btn">6</div>
                <div class="btn" @click="subtract">-</div>
            </div>
            <div class="line4 line">
                <div class="btn">1</div>
                <div class="btn">2</div>
                <div class="btn">3</div>
                <div class="btn" @click="add">+</div>
            </div>
            <div class="line5 line">
                <div class="btn">0</div>
                <div class="btn">.</div>
                <div class="btn" @click="sum()">=</div>
            </div>
        </div>

    </div>
</template>

<script>
    import * as math from 'mathjs'

    export default {
        name: 'calculator-wrapper',
        data() {
            return {
                output: '0',
                input: '',
                num1: 0,
                num2: undefined,
                done: 0,
                mathematical: false,
                mathFunction: null
            }
        },
        mounted() {
            input.addEventListener('click', (x) => {
                this.input = x.target.innerText
                if ('0123456789.'.indexOf(this.input) > -1) {
                    if (!this.mathematical) {
                        if (this.output !== '0'||this.input==='.') {
                            this.output += this.input
                        } else {
                            this.output = this.input
                        }
                        this.num1 = this.isIntOrFloat()
                    } else {
                        if ((this.output !== '0'||this.input==='.')&&this.num2!==undefined) {
                            this.output += this.input
                        } else {
                            this.output = this.input
                        }
                        this.num2 = this.isIntOrFloat()
                    }

                }
            })
        },
        computed: {
            isAC() {
                return this.output !== '0' ? 'C' : 'AC'
            },
            isAdd(){
                let num1 = math.bignumber(this.num1)
                let num2 = math.bignumber(this.num2)
                return math.chain(num1).add(num2)
            },
            isSubtract(){
                let num1 = math.bignumber(this.num1)
                let num2 = math.bignumber(this.num2)
                return math.chain(num1).subtract(num2)
            },
            isMultiply(){
                let num1 = math.bignumber(this.num1)
                let num2 = math.bignumber(this.num2)
                return math.chain(num1).multiply(num2)
            },
            isDivide(){
                let num1 = math.bignumber(this.num1)
                let num2 = math.bignumber(this.num2)
                return math.chain(num1).divide(num2)
            },
            isMod(){
                let num1 = math.bignumber(this.num1)
                let num2 = math.bignumber(this.num2)
                return math.chain(num1).mod(num2)
            }
        },
        methods: {
            isIntOrFloat() {
                return this.output.indexOf('.') <= -1 ? parseInt(this.output) : parseFloat(this.output);
            },
            negate() {
                this.output = (0 - this.isIntOrFloat()).toString()
                if(!this.mathematical){
                    this.num1 = this.isIntOrFloat()
                }else{
                    this.num2 = this.isIntOrFloat()
                }
            },
            mod() {
                this.mathematical = true
                this.sum = ()=>{
                    this.output = (this.isMod.done()).toString()
                }
            },
            multiply() {
                this.mathematical = true
                this.sum = ()=>{
                    this.output = (this.isMultiply.done()).toString()
                }
            },
            subtract() {
                this.mathematical = true
                this.sum = ()=>{
                    this.output = (this.isSubtract.done()).toString()
                }
            },
            divide() {
                this.mathematical = true
                this.sum = ()=>{
                    this.output = (this.isDivide.done()).toString()
                }
            },
            clean() {
                this.output = '0'
                this.num1 = 0
                this.num2 = undefined
                this.mathematical = false
            },
            add() {
                if(this.mathematical){
                    this.sum()
                }
                this.mathematical = true
                this.sum = ()=>{
                    this.output = (this.isAdd.done()).toString()
                    this.mathematical = false
                    this.num1 = this.isIntOrFloat()
                    this.num2 = undefined
                }
            },
            sum() {},
            // open(link) {
            //     this.$electron.shell.openExternal(link)
            // },
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
                    cursor: default;

                    &:active {
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
