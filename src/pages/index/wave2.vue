<template>
    <div @touchmove.prevent>
        <div id="wave2"></div>
    </div>
</template>

<script>
	export default {
		name: "wave2",
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
			var xSpeed = 1;
			var ySpeed = 0.05;
			var xPos = 0;
			var yPos = 0;
			var tempX = 0;
			var tempY = centerY;
			var shape;

            LInit(requestAnimationFrame,'wave2',w,h,function () {
	            setTimeout(function () {
	            	LGlobal.preventDefault = false;
		            main()
	            },0);
            });

            function main() {
            	initBackgroundLayer();
                shape = new LShape();
                backgroundLayer.addChild(shape);
	            backgroundLayer.addEventListener(LEvent.ENTER_FRAME,onframe);
            }

            function onframe() {
                shape.graphics.beginPath();
                shape.graphics.strokeStyle('#000000');
                shape.graphics.lineWidth(1);
                shape.graphics.moveTo(tempX,tempY);
                xPos += xSpeed
                yPos = centerY + Math.sin(angle)*range;
                shape.graphics.lineTo(xPos,yPos);
                shape.graphics.stroke();
                tempX = xPos;
                tempY = yPos;
	            angle += ySpeed;

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
