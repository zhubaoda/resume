<style lang="less" scoped>
.clock {}
</style>
<template>
    <div class="clock">
        <canvas id="c2" :width="param.w" :height="param.h"></canvas>
    </div>
</template>
<script>
export default {
    name: 'clock',
    data() {
        return {

        }
    },
    props: {
        param: {

        }
    },
    methods: {
        getClock() {
            let _self = this;
            var oC = document.getElementById('c2');
            var oGC = oC.getContext('2d'); //获取绘制环境
            oGC.moveTo(0,0);
            //弧度 = 角度*Math.PI/180
            //oGC.arc(200,200,150,0,6*Math.PI/180);
            //oGC.moveTo(200,200);
            //弧度 = 角度*Math.PI/180
            //oGC.arc(200,200,150,6,12*Math.PI/180);
            //oGC.stroke();
            function toDraw() {
                var x = _self.param.w/2;
                var y = _self.param.h/2;
                var r = _self.param.w*2/6;

                //每一次都要清空画布
                oGC.clearRect(0, 0, oGC.width, oGC.height);
                oGC.strokeStyle = "#000";
                //获取当前时间
                var oDate = new Date();
                var oHours = oDate.getHours();
                var oMin = oDate.getMinutes();
                var oSen = oDate.getSeconds();

                var oHoursValue = (-90 + oHours * 30 + (oMin * 6) / 60 + (oSen * 6) / 3600) * Math.PI / 180;
                var oMinValue = (-90 + oMin * 6 + (oSen * 6) / 60) * Math.PI / 180;
                var oSenValue = (-90 + oSen * 6) * Math.PI / 180;


                oGC.beginPath();
                for (var i = 0; i < 60; i++) {
                    oGC.moveTo(x, y);
                    oGC.arc(x, y, r, 6 * i * Math.PI / 180, 6 * (i + 1) * Math.PI / 180);
                }
                oGC.closePath();
                oGC.stroke();


                oGC.fillStyle = 'white';
                oGC.beginPath();
                oGC.arc(x, y, r * (19 / 20), 0, 360 * Math.PI / 180);
                oGC.closePath();
                oGC.fill();


                oGC.beginPath();
                for (var i = 0; i < 12; i++) {
                    oGC.moveTo(x, y);
                    oGC.lineWidth = 2;
                    oGC.arc(x, y, r, 30 * i * Math.PI / 180, 30 * (i + 1) * Math.PI / 180);
                }
                oGC.closePath();
                oGC.stroke();


                oGC.fillStyle = 'white';
                oGC.beginPath();
                oGC.arc(x, y, r * (18 / 20), 0, 360 * Math.PI / 180);
                oGC.closePath();
                oGC.fill();

                //时针
                oGC.beginPath();
                oGC.moveTo(x, y);
                oGC.lineWidth = 5;
                oGC.arc(x, y, r * (10 / 20), oHoursValue, oHoursValue);
                oGC.closePath();
                oGC.stroke();

                //分针
                oGC.beginPath();
                oGC.moveTo(x, y);
                oGC.lineWidth = 3;
                oGC.arc(x, y, r * (14 / 20), oMinValue, oMinValue);
                oGC.closePath();
                oGC.stroke();

                //秒针
                oGC.beginPath();
                oGC.moveTo(x, y);
                oGC.lineWidth = 1;
                oGC.strokeStyle = "red"
                oGC.arc(x, y, r * (17 / 20), oSenValue, oSenValue);
                oGC.closePath();
                oGC.stroke();

            }
            setInterval(toDraw, 1000);
        }
    },
    mounted() {
        this.getClock();

    }
}
</script>
