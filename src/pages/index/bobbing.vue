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
			return {}
        },
		mounted() {
			var backgroundLayer;
			var w = document.body.clientWidth;
			var h = document.body.clientHeight;
			var angle = 0;
			var centerY = h/2;
			var range = 50;
			var speed = 0.1;
			var ball;

            LInit(requestAnimationFrame,'bobbing',w,h,function () {
	            setTimeout(function () {
	            	LGlobal.preventDefault = false;
		            main()
	            },0);
            });

            function main() {
            	initBackgroundLayer();
	            ball = new LSprite();
	            backgroundLayer.addChild(ball);
	            ball.graphics.drawArc(0, '', [0, 0, 20, 0, 2 * Math.PI], true, "#ff0000");
                ball.x = w/2;
                ball.y = h/2;
                backgroundLayer.addEventListener(LEvent.ENTER_FRAME,onframe);
            }

            function onframe() {
	            ball.y = centerY + Math.sin(angle)*range;
	            angle+=speed;
            }

            function initBackgroundLayer() {
	            let s = this;
	            backgroundLayer = new LSprite();
	            addChild(backgroundLayer);
            }
		},
        destroy(){}
	};
</script>

<style scoped>
</style>
