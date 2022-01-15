<!--
 * @Author: chiLi
 * @Date: 2022-01-15 18:19:38
 * @LastEditors: Small electric motor
 * @Description: For reference only
 * @FilePath:: 当乌云散去，自会有繁星出现

    


-->

<template>
    <!-- 验证码组件 -->
    <div id="code">
        <canvas id="canvas"  ref="canvas" width="140" height="37" @click="num"></canvas>
    </div>
</template>

<script>
export default {
    // 创建组件
    name:'Code',
    data () {
        return {
           
        }
    },
    methods:{
        // 随机数生成函数
        rn(min,max){
           return parseInt(Math.random()*(max-min)+min)
        },
        // 随机生成颜色函数
        rc(min,max){
            var r = this.rn(min,max);
            var g = this.rn(min,max);
            var b = this.rn(min,max);
            return `rgb(${r},${g},${b})`
        },
        // 随机生成背景
        bj(){
            // 设置图形的宽高
            var w = 140;
            var h = 37;

            var canvas = document.getElementById('canvas');
            var ctx = canvas.getContext('2d')
            // 在canvans绘制背景颜色
            ctx.fillStyle = this.rc(180,230)
            ctx.fillRect(0,0,w,h)

            // 随机字符串
            var pool = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890'
            var result = ""
            for(var i = 0; i < 4 ; i++){
                // 取出随机的字母或数字
                var c = pool[this.rn(0,pool.length)]
                // 随机出字体大小
                var fs = this.rn(18,40)
                // 随机字母的数字旋转角度
                var deg = this.rn(-30,30)
                ctx.font = fs + 'px Simhei'
                ctx.textBaseLine = 'top';
                // 设置字体的填充颜色
                ctx.fillStyle =this.rc(80,150)
                ctx.save()
                ctx.translate(30*i+15,15)
                ctx.rotate(deg*Math.PI/180)
                // 字体距离
                ctx.fillText(c,-6,14)
                ctx.restore()
                result+=c
            }

            // 随机生成干扰线
            for(var i = 0; i < 5;i++){
                ctx.beginPath();
                ctx.moveTo(this.rn(0,w),this.rn(0,h));
                ctx.lineTo(this.rn(0,w),this.rn(0,h));
                ctx.strokesStyle = this.rc(180,200)
                ctx.closePath();
                ctx.stroke();
            }

            // 随机产生40个小的圆点干扰
            for(var i = 0; i < 40;i++){
                ctx.beginPath();
                ctx.arc(this.rn(0,w),this.rn(0,h),1,0,2*Math.PI);
                ctx.closePath();
                ctx.dillStyle = this.rc(150,200);
                ctx.fill()
            }

            console.log(result)
        },
        // 点击更改数据
        num(){
            this.bj()
        }
    },
    mounted(){
       this.bj()
    },
    created () {
        
    }

}
</script>

<style>

</style>