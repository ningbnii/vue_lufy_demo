<template>
    <div>
        <div id="circle"></div>
    </div>
</template>

<script>
	import Ball from "../../assets/js/ball";

	var backgroundLayer;
	export default {
		name: "circle",
        data(){
		    return {

            }
        },
		mounted() {
			var w = document.body.clientWidth;
			var h = document.body.clientHeight;
			var centerX = w/2;
			var centerY = h/2;
			var shape;
			var shape1;


			LInit(requestAnimationFrame,'circle',w,h,function () {
				setTimeout(function () {
					LGlobal.preventDefault = false;
					main()
				},0);
			});

			function main() {
			    let s = this;
				initBackgroundLayer();
                shape = new LShape();
                backgroundLayer.addChild(shape);
                shape.graphics.drawRect(1,'#000000',[-2,-2,4,4],true,'#ffffff');
                shape.x = centerX;
                shape.y = centerY;

                shape1 = new LShape();
                backgroundLayer.addChild(shape1);

				backgroundLayer.addEventListener(LMouseEvent.MOUSE_MOVE,onMouseMove);
			}

			function onMouseMove(e) {
			    shape1.graphics.clear();
                shape1.graphics.beginPath();
                shape1.graphics.strokeStyle('#ff0000');
                shape1.graphics.moveTo(shape.x,shape.y);
                shape1.graphics.lineTo(e.selfX,e.selfY);
                shape1.graphics.stroke();
			}

			function initBackgroundLayer() {
				let s = this;
				backgroundLayer = new LSprite();
				backgroundLayer.graphics.drawRect(0,'',[0,0,w,h],true,'#ffffff');
				addChild(backgroundLayer);
			}
		},
		methods: {

		},
        destroyed(){
		    // 页面销毁前，必须把backgroundLayer移除，否则，再次进入会报错
            backgroundLayer.removeAllEventListener();
            removeChild(backgroundLayer)
        }
	};
</script>

<style scoped>
</style>
