<template>
    <div @touchmove.prevent>
        <div id="random"></div>
    </div>
</template>

<script>
	import Ball from "../../assets/js/ball";

	export default {
		name: "random",
        data(){
			return {
			    backgroundLayer:{},
            }
        },
		mounted() {
			var s = this;
			var w = document.body.clientWidth;
			var h = document.body.clientHeight;
			var angleX = 0;
			var angleY = 0;
			var centerX = w/2;
			var centerY = h/2;
			var range = 50;
			var xSpeed = 0.07;
			var ySpeed = 0.11;
			var ball;

            LInit(requestAnimationFrame,'random',w,h,function () {
	            setTimeout(function () {
	            	LGlobal.preventDefault = false;
		            main()
	            },0);
            });

            function main() {
            	initBackgroundLayer();
	            ball = new LSprite();
	            s.backgroundLayer.addChild(ball);
	            ball.graphics.drawArc(0, '', [0, 0, 20, 0, 2 * Math.PI], true, "#ff0000");
                ball.x = w/2;
                ball.y = h/2;
                s.backgroundLayer.addEventListener(LEvent.ENTER_FRAME,onframe);
            }

            function onframe() {
	            ball.x = centerX + Math.sin(angleX)*range;
	            ball.y = centerY + Math.sin(angleY)*range;
	            angleX+=xSpeed;
	            angleY+=ySpeed;
            }

            function initBackgroundLayer() {
	            s.backgroundLayer = new LSprite();
	            addChild(s.backgroundLayer);
            }
		},
        destroyed(){
		    removeChild(this.backgroundLayer);
        }
	};
</script>

<style scoped>
</style>
