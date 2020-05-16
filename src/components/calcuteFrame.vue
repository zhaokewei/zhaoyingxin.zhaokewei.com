<template>
    <div class="component">
        <div class="title">
            小仙女专属计算器
        </div>
        <form>
            <fieldset>
                <div class="config">
                    <div class="framePerseconds">
                        <label>每秒帧数</label>
                        <input
                            id="fps-input"
                            class="num-input"
                            v-model.number="framePerSecond"
                            type="number">
                    </div>
                </div>
                <div class="frameInput">
                    <label>帧位置</label>
                    <input type="number" :min="0" v-model.number="hour">:
                    <input type="number" :min="0" v-model.number="min">:
                    <input type="number" :min="0" v-model.number="sec">&nbsp;
                    <input type="number" :min="0" v-model.number="pos">
                </div>
                <div class="result">
                    {{ parseInt(dst / framePerSecond / 60 / 60)}}:{{ parseInt(dst / framePerSecond / 60 % 60)}}:{{ parseInt(dst / framePerSecond % 60)}}  {{dst % framePerSecond}}
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
                framePerSecond: 25,
                hour: 0,
                min: 0,
                sec: 0,
                pos: 0
            }
        },
        computed: {
            dst: function () {
                return parseInt((this.hour * 3600 + this.min * 60 + this.sec) * this.framePerSecond + this.pos)
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

        background: pink;
        border-radius: 30px;
    }
    .num-input {

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
        width: 80px;
        vertical-align: center;
        margin-right: 2px;
    }
    .result {
        padding: 3px 6px;
        color: fuchsia;
        font-size: 2em;
    }

    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button{
        -webkit-appearance: none !important;
        margin: 0;
    }
    input[type="number"]{-moz-appearance:textfield;}

    input {
        width: 40px;
    }


</style>