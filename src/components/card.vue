<style lang="less" scoped>
.card {
    width: 100%;
    position: relative;
    .tab{
        width: 80%;
        height: 50px;
        background-color: #fa6705;
        color: #fff;
        font-size: 25px;
        text-align: center;
        border-radius: 25px;
        line-height: 50px;
        margin: 50px auto;
    }
    #c3 {
        background: #fff url('/static/icon/1111.png') no-repeat;
        background-size:100% 100%;
    }
}
</style>
<template>
    <div class="card">
        <div class="tab" @click="getCanvas" v-show="!show">
            点击刮刮乐
        </div>
        <canvas id="c3" width="200" height="100" @touchstart="touchstart" @touchmove="touchmove" @touchend="touchend" v-show="show"></canvas>
    </div>
</template>
<script>
export default {
    name: 'card',
    data() {
        return {
            show: false
        }
    },
    props: {
        param: {

        }
    },
    methods: {
        touchstart(ev) {
            var oC = document.getElementById('c3');
            var oCc = oC.getContext('2d'); //获取绘制环境
            var ev = ev || window.event;
            oCc.moveTo(ev.clientX - oC.offsetLeft, ev.clientY - oC.offsetTop);
        },
        touchmove(ev) {
            var oC = document.getElementById('c3');
            var oCc = oC.getContext('2d'); //获取绘制环境
            var ev = ev || window.event;
            console.log(ev.touches[0].clientX);
            // oCc.strokeStyle = "#000";
            // oCc.lineWidth = 10;
            // oCc.lineTo(ev.touches[0].clientX - oC.offsetLeft, ev.touches[0].clientY - oC.offsetTop);
            // oCc.stroke();
            var W = 10;
            var H = 10;
            oCc.clearRect(ev.touches[0].clientX - oC.offsetLeft, ev.touches[0].clientY - oC.offsetTop,W,H)
        },
        touchend() {
            document.onmousemove = null;
            document.onmouseup = null;
            var oC = document.getElementById('c3');
            var oCc = oC.getContext('2d'); //获取绘制环境      
        },
        getCanvas() {
            this.show = true;
            var oC = document.getElementById('c3');
            var oCc = oC.getContext('2d'); //获取绘制环境
            oCc.fillStyle = "red"; //填充颜色
            oCc.fillRect(0, 0, this.param.w, this.param.h); //绘制方块
        }
    },
    created() {

    },
    mounted() {

    }
}
</script>
