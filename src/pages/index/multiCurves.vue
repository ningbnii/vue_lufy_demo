<template>
    <div @touchmove.prevent>
        <van-button type="primary" class="control" @click="changeCloseStatus()">是否闭合：{{closeStatus ? '是' : '否'}}
        </van-button>
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
                numPoints: 3,
                closeStatus: false,
            }
        },
        mounted() {
            let s = this;
            const w = document.body.clientWidth;
            const h = document.body.clientHeight;
            let shape = {}, textLayer = {};
            let points = {};

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
                textLayer = new LSprite();
                s.backgroundLayer.addChild(textLayer);

                create()

            }

            function create() {
                shape.graphics.clear();
                textLayer.removeAllChild();
                // 创建由随机点组成的一个数组
                for (let i = 0; i < s.numPoints; i++) {
                    let tempX = Math.random() * w;
                    let tempY = Math.random() * h;
                    points[i] = {
                        x: tempX,
                        y: tempY,
                    }
                    // 绘制点
                    shape.graphics.drawArc(0, '', [tempX, tempY, 10, 0, 2 * Math.PI], true, '#ff0000');
                    // 绘制数字
                    let text = new LTextField();
                    textLayer.addChild(text);
                    text.text = i + 1;
                    text.x = tempX - 5;
                    text.y = tempY - 8;
                    text.size = 18;
                    text.color = '#ffffff';
                }
                // 绘制曲线
                shape.graphics.add(function (ctx) {

                    ctx.beginPath();
                    if (s.closeStatus) {
                        // 闭合
                        // 以第一个点和最后一个点的终点作为开始点
                        let xc1 = (points[0].x + points[s.numPoints - 1].x) / 2;
                        let yc1 = (points[0].y + points[s.numPoints - 1].y) / 2;
                        ctx.moveTo(xc1,yc1);
                        let i;
                        for(i=0;i<s.numPoints-1;i++){
                            let xc = (points[i].x + points[i + 1].x) / 2;
                            let yc = (points[i].y + points[i + 1].y) / 2;
                            ctx.quadraticCurveTo(points[i].x, points[i].y, xc, yc);
                        }
                        // 以开始点作为终点
                        ctx.quadraticCurveTo(points[i].x, points[i].y, xc1, yc1);
                    } else {
                        // 非闭合
                        // 以第一个点作为开始点
                        ctx.moveTo(points[0].x, points[0].y);
                        let i = 1;
                        for (i = 1; i < s.numPoints - 2; i++) {
                            let xc = (points[i].x + points[i + 1].x) / 2;
                            let yc = (points[i].y + points[i + 1].y) / 2;
                            // 以points[i] 作为中间控制点，points[i] 和 points[i+1]的中心点作为结束点
                            ctx.quadraticCurveTo(points[i].x, points[i].y, xc, yc);
                            // 如果让曲线通过points[i]
                            // let xc1 = 2 * points[i].x - (points[i+1].x + points[i - 1].x) / 2;
                            // let yc1 = 2 * points[i].y - (points[i+1].y + points[i - 1].y) / 2;
                            // ctx.quadraticCurveTo(xc1, yc1, points[i+1].x, points[i+1].y);
                        }
                        // 以最后一个点作为结束点
                        ctx.quadraticCurveTo(points[i].x, points[i].y, points[i + 1].x, points[i + 1].y);
                    }

                    ctx.stroke();
                })
            }

            function initBackgroundLayer() {
                s.backgroundLayer = new LSprite();
                s.backgroundLayer.graphics.drawRect(0, '', [0, 0, w, h], true, '#ffffff');
                addChild(s.backgroundLayer);
            }
        },
        methods: {
            changeCloseStatus(){
                this.closeStatus = !this.closeStatus;
            }
        },
        destroyed() {
            removeChild(this.backgroundLayer);
        }
    };
</script>

<style scoped>

</style>
