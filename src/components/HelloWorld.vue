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
        draw(x, y, angle, width, size, color1 = "#0F0") {
            ctx.beginPath();
            ctx.save();
            ctx.strokeStyle = color1;
            ctx.lineWidth = width;
            ctx.translate(x, y);
            ctx.moveTo(0, 0);
            ctx.rotate((angle * Math.PI) / 180);
            ctx.lineTo(0, -size);
            ctx.stroke();

            if (size < 9) {
                ctx.restore();
                return;
            }

            this.draw(0, -size, angle + 8, width * 0.7, size * 0.82);
            this.draw(0, -size, angle - 8, width * 0.7, size * 0.82);
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
