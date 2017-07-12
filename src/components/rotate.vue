<style lang="less" scoped>
.rotate {}
</style>
<template>
    <div class="rotate">
        <canvas id="c1" :width="param.w" :height="param.h"></canvas>
    </div>
</template>
<script>
export default {
    name: 'rotate',
    data() {
        return {
            
        }
    },
    props:{
        param:{

        }
    },
    methods: {
        getCanvas() {
            var oC = document.getElementById('c1');
            var oGC = oC.getContext('2d'); //获取绘制环境
            //translate 从起始点为基准点，移到当前坐标位置
            //rotate 旋转：参数为弧度  例子：旋转的小方块
            //scale 缩放的例子：旋转加缩放的小方块
            var num = 0;
            var num2 = 0;
            var value = 1;

            function toDraw() {
                num++;
                oGC.save();
                oGC.clearRect(0, 0, oC.width, oC.height);
                oGC.translate(oC.width/2, oC.height/2);
                if (num2 == 100) {
                    value = -1;
                } else if (num2 == 0) {
                    value = 1;
                }
                num2 += value;
                oGC.scale(num2 * 1 / 50, num2 * 1 / 50);
                oGC.rotate(num * Math.PI / 180);
                oGC.translate(-50, -50);
                oGC.fillRect(0, 0, 100, 100);
                oGC.restore();
            }
            setInterval(toDraw, 30);
            // oGC.rotate(45 * Math.PI / 180);
            // oGC.scale(1, 1); //宽和高
            // oGC.fillRect(0, 0, 100, 100);
        }
    },
    mounted() {
        this.getCanvas();

    }
}
</script>
