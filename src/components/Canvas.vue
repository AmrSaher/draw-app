<template>
    <div class="board-container">
        <canvas id="board"></canvas>
    </div>
</template>

<script>
export default {
    name: "Canvas",
    props: ['tool', 'fillColor', 'size'],
    mounted() {
        this.canvas = document.querySelector("#board");
        this.ctx = this.canvas.getContext("2d");

        this.prevMouseX = null;
        this.prevMouseY = null;
        this.snapshot = "";
        this.isDrawing = false;

        window.addEventListener("load", () => {
            this.canvas.width = this.canvas.offsetWidth;
            this.canvas.height = this.canvas.offsetHeight;
        });

        this.canvas.addEventListener("mousedown", this.startDraw);
        this.canvas.addEventListener("mouseup", () => { this.isDrawing = false; });
        this.canvas.addEventListener("mousemove", this.drawing);
    },
    methods: {
        drawing(e) {
            if (!this.isDrawing) return;
            this.ctx.putImageData(this.snapshot, 0, 0);
            
            if (this.tool == "brush") {
                this.ctx.strokeStyle = "#fff";
                this.ctx.lineTo(e.offsetX, e.offsetY);
                this.ctx.stroke();
            } else if (this.tool == "square") {
                this.drawRect(e);
            } else if (this.tool == "circle") {
                this.drawCircle(e);
            } else if (this.tool == "triangle") {
                this.drawTriangle(e);
            }
        },
        startDraw(e) {
            this.isDrawing = true;
            this.prevMouseX = e.offsetX;
            this.prevMouseY = e.offsetY;
            this.ctx.beginPath();
            this.ctx.lineWidth = this.size;
            this.snapshot = this.ctx.getImageData(0, 0, this.canvas.width, this.canvas.height);
        },
        drawRect(e) {
            if (!this.fillColor) {
                return this.ctx.strokeRect(e.offsetX, e.offsetY, this.prevMouseX - e.offsetX, this.prevMouseY - e.offsetY);
            }
            return this.ctx.fillRect(e.offsetX, e.offsetY, this.prevMouseX - e.offsetX, this.prevMouseY - e.offsetY);
        },
        drawCircle(e) {
            this.ctx.beginPath();
            let radius = Math.sqrt(Math.pow((this.prevMouseX - e.offsetX), 2) + Math.pow((this.prevMouseY - e.offsetY), 2));
            this.ctx.arc(this.prevMouseX, this.prevMouseY, radius, 0, Math.PI * 2);
            this.fillColor ? this.ctx.fill() : this.ctx.stroke();
        },
        drawTriangle(e) {
            this.ctx.beginPath();
            this.ctx.moveTo(this.prevMouseX, this.prevMouseY);
            this.ctx.lineTo(e.offsetX, e.offsetY);
            this.ctx.lineTo(this.prevMouseX * 2 - e.offsetX, e.offsetY);
            this.ctx.closePath();
            this.fillColor ? this.ctx.fill() : this.ctx.stroke();
        }
    }
};
</script>

<style lang="scss" scoped>
.board-container {
    // overflow: auto;
    width: 100%;
    height: calc(100% - 68px);
    #board {
        width: 100%;
        height: 100%;
    }
}
</style>