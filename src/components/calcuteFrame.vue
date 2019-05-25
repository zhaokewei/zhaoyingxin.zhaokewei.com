<template>
    <div class="component">
        <div class="title">
            小仙女专属计算器
        </div>
        <form>
            <fieldset>
                <div class="config">
                    <div class="framePerseconds">
                        <label for="fps-input">每秒帧数</label>
                        <input
                                id="fps-input"
                                class="num-input"
                                v-model="framePerSecond"
                               onkeyup="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
                               onafterpaste="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'0')}else{this.value=this.value.replace(/\D/g,'')"
                               type="number">
                    </div>
                </div>
                <div class="frameInput">
                    <label for="pos-input">帧位置</label>
                    <input
                            id="pos-input"
                            class="num-input"
                            empty
                            v-model="srcPosition"
                            onkeyup="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'')}else{this.value=this.value.replace(/\D/g,'')}"
                            onafterpaste="if(this.value.length==1){this.value=this.value.replace(/[^1-9]/g,'0')}else{this.value=this.value.replace(/\D/g,'')}"
                            autofocus placeholder="请输入帧位置" type="number" />
                </div>
                <div class="result">
                    {{formatDst}}
                </div>
            </fieldset>
        </form>
    </div>
</template>

<script>
    export default {
        name: "calcuteFrame",
        data: function () {
            return {
                srcPosition: NaN,
                dstSeconds: 0,
                dstPosition: 0,
                framePerSecond: 25
            }
        },
        watch: {
            srcPosition: function () {
                this.calcuteDst()
            },
            framePerSecond: function () {
                this.calcuteDst()
            }
        },
        computed: {
            formatDst: function () {
                let timeFmt = this.formatTime(this.dstSeconds)
                return `${timeFmt} ${this.dstPosition}帧`
            }
        },
        methods: {
            formatTime: function (value) {
                let hours =  Math.floor(value / 3600);
                value = value % 3600
                let minutes = Math.floor(value / 60);
                let seconds= value % 60;

                let dHours = (hours > 9 ? hours : '0' + hours);
                let dMins = (minutes > 9 ? minutes : '0' + minutes);
                let dSecs = (seconds > 9 ? seconds : '0' + seconds);

                return dHours + ":" + dMins + ":" + dSecs;
            },
            calcuteDst: function () {
                if(this.framePerSecond <= 0) this.framePerSecond = 1
                let seconds = Math.floor(this.srcPosition / this.framePerSecond)
                let dstPosition = this.srcPosition % this.framePerSecond
                this.dstSeconds = seconds
                this.dstPosition = dstPosition
            }
        }
    }
</script>

<style scoped>
    .title {
        margin: 30px;
        font-size: 2em;
        color: fuchsia;
    }
    .component {
        font-size: 2em;
        background: pink;
        border-radius: 30px;
    }
    .num-input {
        font-size: 1em;
    }
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        /* display: none; <- Crashes Chrome on hover */
        -webkit-appearance: none;
        margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
        font-size: inherit;
    }

    input[type=number] {
        -moz-appearance:textfield; /* Firefox */
    }
    fieldset {
        border: none;
        border-radius: 2px;
        margin-bottom: 12px;
        overflow: hidden;
        padding: 0 .625em;
    }
    label {
        cursor: pointer;
        display: inline-block;
        padding: 3px 6px;
        text-align: right;
        width: 150px;
        vertical-align: top;
        margin-right: 2px;
    }
    .result {
        padding: 3px 6px;
        color: fuchsia;
        font-size: 3em;
    }
</style>