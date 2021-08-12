<template>
<!-- @touchmove.prevent禁止页面拖拽   -->
    <div @touchmove.prevent>
        <span class="float">{{num}}</span>
        <div id="circle"></div>
    </div>
</template>

<script>
    import Ball from "../../assets/js/ball";

    export default {
        name: "circle",
        data() {
            return {
                backgroundLayer: {},
                num: 0,
            }
        },
        mounted() {
            let s = this;
            var w = document.body.clientWidth;
            var h = document.body.clientHeight;
            var centerX = w / 2;
            var centerY = h / 2;
            var shape;
            var shape1;

            LInit(requestAnimationFrame, 'circle', w, h, function () {
                setTimeout(function () {
                    LGlobal.preventDefault = false;
                    main()
                }, 0);
            });

            function main() {
                initBackgroundLayer();
                shape = new LShape();
                s.backgroundLayer.addChild(shape);
                shape.graphics.drawRect(1, '#000000', [-2, -2, 4, 4], true, '#ffffff');
                shape.x = centerX;
                shape.y = centerY;

                shape1 = new LShape();
                s.backgroundLayer.addChild(shape1);

                s.backgroundLayer.addEventListener(LMouseEvent.MOUSE_MOVE, onMouseMove);
            }

            function onMouseMove(e) {
                shape1.graphics.clear();
                shape1.graphics.beginPath();
                shape1.graphics.strokeStyle('#ff0000');
                shape1.graphics.moveTo(shape.x, shape.y);
                shape1.graphics.lineTo(e.selfX, e.selfY);
                shape1.graphics.stroke();

                var dx = shape.x - e.selfX;
                var dy = shape.y - e.selfY;
                var dist = Math.sqrt(dx * dx + dy * dy);
                s.num = dist.toFixed(2).toString();
            }

            function initBackgroundLayer() {
                s.backgroundLayer = new LSprite();
                s.backgroundLayer.graphics.drawRect(0, '', [0, 0, w, h], true, '#ffffff');
                addChild(s.backgroundLayer);
            }
        },
        methods: {},
        destroyed() {
            // 页面销毁前，必须把backgroundLayer移除，否则，再次进入会报错
            removeChild(this.backgroundLayer)
        }
    };
</script>

<style scoped>
    .float {
        float: left;
        z-index: 1000;
        position: absolute;
    }
</style>
