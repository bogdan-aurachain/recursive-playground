<template>
    <div class="hello">
        <canvas ref="canvas"></canvas>
    </div>
</template>

<script>
let ctx;
export default {
    name: "HelloWorld",
    props: {
        msg: String
    },
    mounted() {
        const { canvas } = this.$refs;
        canvas.width = 500;
        canvas.height = 500;
        ctx = canvas.getContext("2d");

        this.draw(canvas.width / 2, canvas.height, 0, 20, 90);
    },
    methods: {
        draw(x, y, angle, width, size, color1 = "#0F0", color2 = "#F00") {
            ctx.beginPath();
            ctx.save();
            ctx.strokeStyle = color1;
            ctx.fillStyle = color2;
            ctx.lineWidth = width;
            ctx.translate(x, y + 5); // added +5 so that the branches will be more compact
            ctx.moveTo(0, 0);
            ctx.rotate((angle * Math.PI) / 180);
            if (angle > 0) {
                // right branch
                ctx.bezierCurveTo(5, -size / 2, 10, -size / 2, 0, -size);
            } else {
                // left branch
                ctx.bezierCurveTo(5, -size / 2, -10, -size / 2, 0, -size);
            }
            ctx.stroke();

            if (size < 9) {
                // last draw will be the leaf
                ctx.beginPath();
                ctx.arc(0, -size, 10, 0, Math.PI / 2.2);
                ctx.fill();
                ctx.restore();
                return;
            }

            // some randomness to the branch curve as suggested
            const curve = (Math.random() * 10) + 10;
            this.draw(0, -size, angle + curve, width * 0.7, size * 0.82);
            this.draw(0, -size, angle - curve, width * 0.7, size * 0.82);
            ctx.restore();
        }
    }
};
</script>

<style lang="scss">
html {
    background-color: gray;
}

canvas {
    background-color: black;
}
</style>
