<template>
    <ul class="nav d-flex justify-content-center align-items-center">
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-cursor-fill" @click="selectTool('mouse')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-brush-fill" @click="selectTool('brush')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-eraser-fill" @click="selectTool('eraser')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-square" @click="selectTool('square')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-circle" @click="selectTool('circle')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-triangle" @click="selectTool('triangle')"></i>
            </span>
        </li>
        <li class="nav-item" @click="fullscreen">
            <span class="nav-link">
                <i class="bi bi-fullscreen"></i>
            </span>
        </li>
        <li class="nav-item dropdown">
            <span class="nav-link dropdown-toggle" data-bs-toggle="dropdown" role="button" aria-expanded="false">Size</span>
            <ul class="dropdown-menu bg-dark">
                <li>
                    <input type="number" class="form-control bg-dark text-white" v-model="size" @change="setSize">
                </li>
            </ul>
        </li>
        <li class="nav-item dropdown">
            <span class="nav-link dropdown-toggle" data-bs-toggle="dropdown" role="button" aria-expanded="false">Color</span>
            <ul class="dropdown-menu bg-dark">
                <li>
                    <input type="color" class="form-control bg-dark text-white" v-model="color" @change="selectColor">
                </li>
            </ul>
        </li>
        <li class="nav-item dropdown">
            <span class="nav-link dropdown-toggle" data-bs-toggle="dropdown" role="button" aria-expanded="false">Fill color</span>
            <ul class="dropdown-menu bg-dark text-center">
                <input type="checkbox" class="bg-dark text-white w-20" v-model="isFill" @change="fillColor">
            </ul>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-file-minus" @click="selectTool('clear')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-box-arrow-down" @click="selectTool('download')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-plus" @click="selectTool('zoomIn')"></i>
            </span>
        </li>
        <li class="nav-item">
            <span class="nav-link">
                <i class="bi bi-dash" @click="selectTool('zoomOut')"></i>
            </span>
        </li>
    </ul>
</template>

<script>
export default {
    name: 'DrawNav',
    data() {
        return {
            isFull: false,
            size: 5,
            color: "white",
            isFill: false
        };
    },
    methods: {
        fullscreen() {
            if (this.isFull) {
                document.exitFullscreen();
            } else {
                document.body.requestFullscreen();
            }
            this.isFull = !this.isFull;
            this.$emit("changeWindowSize");
        },
        selectTool(tool) {
            this.$emit("selectTool", tool);
        },
        fillColor() {
            this.$emit("fillColor", this.isFill);
        },
        setSize() {
            this.$emit("changeSize", this.size);
        },
        selectColor() {
            this.$emit("color", this.color);
        }
    }
};
</script>

<style lang="scss" scoped>
.nav {
    padding: 6px 0;
    border-bottom: 1px solid #999;
    flex-wrap: nowrap;
    .form-control-color {
        width: 25px;
        height: 25px;
        padding: 5px;
    }
    i {
        font-size: 20px;
    }
}
</style>