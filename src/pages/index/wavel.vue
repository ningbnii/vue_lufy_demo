<template>
    <div>
        <div id="wavel"></div>
    </div>
</template>

<script>
	import Ball from "../../assets/js/ball";

	export default {
		name: "wavel",
		mounted() {
			var backgroundLayer;
			var w = document.body.clientWidth;
			var h = document.body.clientHeight;
			var angle = 0;
			var centerY = h/2;
			var range = 100;
			var xspeed = 1;
			var yspeed = 0.05;
			var ball;

			LInit(requestAnimationFrame,'wavel',w,h,function () {
				setTimeout(function () {
					LGlobal.preventDefault = false;
					main()
				},0);
			});

			function main() {
				initBackgroundLayer();
				ball = new Ball();
				backgroundLayer.addChild(ball);
				
				ball.x = 0;
				ball.y = h/2;
				backgroundLayer.addEventListener(LEvent.ENTER_FRAME,onframe);
			}

			function onframe() {
				ball.x += xspeed;
				ball.y = centerY + Math.sin(angle) * range;
				angle+= yspeed;
			}

			function initBackgroundLayer() {
				let s = this;
				backgroundLayer = new LSprite();
				addChild(backgroundLayer);
			}
		},
		methods: {

		}
	};
</script>

<style scoped>
</style>
