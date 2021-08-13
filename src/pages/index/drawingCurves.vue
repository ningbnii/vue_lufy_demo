<template>
    <div @touchmove.prevent>
        <div id="drawingCurves"></div>
    </div>
</template>

<script>
    import Ball from "../../assets/js/ball";

    export default {
        name: "drawingCurves",
        data() {
            return {
                backgroundLayer: {},
            }
        },
        mounted() {
            let s = this;
            const w = document.body.clientWidth;
            const h = document.body.clientHeight;
            // 起点
            let x0 = 100;
            let y0 = 200;
            // 控制点
            let x1 = 0;
            let y1 = 0;
            // 终点
            let x2 = 300;
            let y2 = 200;
            // 按下状态
            let down = false;
            let shape = {};
            let pointShape = {};

            LInit(requestAnimationFrame, 'drawingCurves', w, h, function () {
                setTimeout(function () {
                    LGlobal.preventDefault = false;
                    main()
                }, 0);
            });

            function main() {
                initBackgroundLayer();
                shape = new LShape();
                s.backgroundLayer.addChild(shape);
                pointShape = new LShape();
                s.backgroundLayer.addChild(pointShape);

                /**
                 * add中的变量值改变，曲线会重新绘制，感觉add在一直在绘制
                 */
                shape.graphics.add(function (ctx) {
                    ctx.beginPath();
                    ctx.moveTo(x0, y0);
                    ctx.quadraticCurveTo(x1, y1, x2, y2);
                    ctx.stroke();
                })


                s.backgroundLayer.addEventListener(LMouseEvent.MOUSE_DOWN, onMouseDown);
                s.backgroundLayer.addEventListener(LMouseEvent.MOUSE_MOVE, onMouseMove);
                s.backgroundLayer.addEventListener(LMouseEvent.MOUSE_UP, onMouseUp);
                // s.backgroundLayer.addEventListener(LEvent.ENTER_FRAME,frame);
            }


            function onMouseDown(e) {
                down = true;

                pointShape.graphics.drawArc(0, '', [e.selfX, e.selfY, 5, 0, 2 * Math.PI], true, '#ff0000');
            }

            function onMouseMove(e) {
                if (down) {
                    // 设置控制点为当前位置
                    // x1 = e.selfX;
                    // y1 = e.selfY;
                    x1 = e.selfX * 2 - (x0 + x2) / 2;
                    y1 = e.selfY * 2 - (y0 + y2) / 2;
                    //
                    // // 绘制控制点
                    pointShape.graphics.clear();
                    pointShape.graphics.drawArc(0, '', [e.selfX, e.selfY, 5, 0, 2 * Math.PI], true, '#ff0000');
                }
            }

            function onMouseUp(e) {
                down = false;
            }

            function initBackgroundLayer() {
                s.backgroundLayer = new LSprite();
                s.backgroundLayer.graphics.drawRect(0, '', [0, 0, w, h], true, '#ffffff');
                addChild(s.backgroundLayer);
            }
        },
        methods: {},
        destroyed() {
            removeChild(this.backgroundLayer);
        }
    };
</script>

<style scoped>

</style>
