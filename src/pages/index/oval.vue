<template>
    <div @touchmove.prevent>
        <div id="circle"></div>
    </div>
</template>

<script>
	import Ball from "../../assets/js/ball";

	export default {
		name: "circle",
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
			var centerX = w/2;
			var centerY = h/2;
			var radiusX = 200;
			var radiusY = 100;
			var speed = 0.05;
			var ball;

			LInit(requestAnimationFrame,'circle',w,h,function () {
				setTimeout(function () {
					LGlobal.preventDefault = false;
					main()
				},0);
			});

			function main() {
				initBackgroundLayer();
				ball = new Ball();
				s.backgroundLayer.addChild(ball);

				s.backgroundLayer.addEventListener(LEvent.ENTER_FRAME,onframe);
			}

			function onframe() {
				ball.x = centerX + Math.sin(angle) * radiusX;
				ball.y = centerY + Math.cos(angle) * radiusY;
				angle += speed;
			}

			function initBackgroundLayer() {
				s.backgroundLayer = new LSprite();
				addChild(s.backgroundLayer);
			}
		},
		methods: {

		},
        destroyed(){
		    removeChild(this.backgroundLayer);
        }
	};
</script>

<style scoped>
</style>
