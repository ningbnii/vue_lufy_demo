<template>
    <div @touchmove.prevent>
        <div id="pulse"></div>
    </div>
</template>

<script>
	import Ball from "../../assets/js/ball";

	export default {
		name: "pulse",
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
			var centerScale = 1;
			var range = 1;
			var speed = 0.05;
			var ball;

            LInit(requestAnimationFrame,'pulse',w,h,function () {
	            setTimeout(function () {
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
	            ball.scaleX = ball.scaleY = centerScale + Math.sin(angle)*range;
	            angle+=speed;
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
