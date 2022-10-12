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
                <li v-for="i in 15" :key="i" @click="setSize(i)"><a class="dropdown-item text-white">{{ i }}</a></li>
            </ul>
        </li>
        <li class="nav-item dropdown">
            <span class="nav-link dropdown-toggle" data-bs-toggle="dropdown" role="button" aria-expanded="false">Color</span>
            <ul class="dropdown-menu bg-dark">
                <li><a class="dropdown-item text-white" @click="selectColor('red')">Red</a></li>
                <li><a class="dropdown-item text-white" @click="selectColor('blue')">Blue</a></li>
                <li><a class="dropdown-item text-white" @click="selectColor('yellow')">Yellow</a></li>
                <li><a class="dropdown-item text-white" @click="selectColor('white')">White</a></li>
            </ul>
        </li>
        <li class="nav-item dropdown">
            <span class="nav-link dropdown-toggle" data-bs-toggle="dropdown" role="button" aria-expanded="false">Fill color</span>
            <ul class="dropdown-menu bg-dark">
                <li><a class="dropdown-item text-white" @click="fillColor(true)">enable</a></li>
                <li><a class="dropdown-item text-white" @click="fillColor(false)">disable</a></li>
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
    </ul>
</template>

<script>
export default {
    name: 'DrawNav',
    data() {
        return {
            isFull: false
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
        fillColor(is) {
            this.$emit("fillColor", is);
        },
        setSize(s) {
            this.$emit("changeSize", s);
        },
        selectColor(c) {
            this.$emit("color", c);
        }
    }
};
</script>

<style lang="scss" scoped>
.nav {
    padding: 6px 0;
    border-bottom: 1px solid #999;
    flex-wrap: nowrap;
    // position: fixed;
    // width: 100%;
    // z-index: 9999;
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