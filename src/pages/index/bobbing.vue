<template>
    <div @touchmove.prevent>
        <div id="bobbing"></div>
    </div>
</template>

<script>
	import Ball from "../../assets/js/ball";

	export default {
		name: "bobbing",
        data(){
			return {
			    backgroundLayer:{},
            }
        },
		mounted() {
            let s = this;
			var w = document.body.clientWidth;
			var h = document.body.clientHeight;
			var angle = 0;
			var centerY = h/2;
			var range = 50;
			var speed = 0.1;
			var ball;

            LInit(requestAnimationFrame,'bobbing',w,h,function () {
	            setTimeout(function () {
					// 移动网页中用来禁止滚屏，默认为true(禁止)，如果需要使用滚屏功能，则需要将其设置为fasle
					// 如果不设置preventDefault=false，返回上一页，页面不能点击
	            	LGlobal.preventDefault = false;
		            main()
	            },0);
            });

            function main() {
            	initBackgroundLayer();
	            ball = new Ball();
	            s.backgroundLayer.addChild(ball);
	        
                ball.x = w/2;
                ball.y = h/2;
                s.backgroundLayer.addEventListener(LEvent.ENTER_FRAME,onframe);
            }

            function onframe() {
	            ball.y = centerY + Math.sin(angle)*range;
	            angle+=speed;
            }

            function initBackgroundLayer() {
	            let s = this;
	            s.backgroundLayer = new LSprite();
	            addChild(s.backgroundLayer);
            }
		},
        destroyed(){
            removeChild(this.backgroundLayer)
        }
	};
</script>

<style scoped>
</style>
