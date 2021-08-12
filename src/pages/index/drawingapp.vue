<template>
    <div @touchmove.prevent>
        <div id="drawingapp"></div>
    </div>
</template>

<script>
	import Ball from "../../assets/js/ball";

	export default {
		name: "drawingapp",
        data(){
		    return {
		        backgroundLayer:{},
            }
        },
		mounted() {
			let s = this;
            const w = document.body.clientWidth;
            const h = document.body.clientHeight;
            let tempX = 0;
            let tempY = 0;
            let down = false;
            let shape = {};

            LInit(requestAnimationFrame,'drawingapp',w,h,function () {
				setTimeout(function () {
					LGlobal.preventDefault = false;
					main()
				},0);
			});

			function main() {
				initBackgroundLayer();
                shape = new LShape();
                s.backgroundLayer.addChild(shape);

				s.backgroundLayer.addEventListener(LMouseEvent.MOUSE_DOWN,onMouseDown);
				s.backgroundLayer.addEventListener(LMouseEvent.MOUSE_MOVE,onMouseMove);
				s.backgroundLayer.addEventListener(LMouseEvent.MOUSE_UP,onMouseUp);
			}

			function onMouseDown(e) {
                down = true;
                tempX = e.selfX;
                tempY = e.selfY;
            }

            function onMouseMove(e) {
                if(down){
                    shape.graphics.beginPath();
                    shape.graphics.moveTo(tempX,tempY);
                    shape.graphics.lineTo(e.selfX,e.selfY);
                    shape.graphics.stroke();
                    tempX = e.selfX;
                    tempY = e.selfY;
                }
            }

            function onMouseUp(e) {
                down = false;
            }

			function initBackgroundLayer() {
				s.backgroundLayer = new LSprite();
				s.backgroundLayer.graphics.drawRect(0,'',[0,0,w,h],true,'#ffffff');
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
