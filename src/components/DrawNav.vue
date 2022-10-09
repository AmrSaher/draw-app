<template>
    <ul class="nav d-flex justify-content-center align-items-center">
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-cursor-fill" @click="selectTool('mouse')"></i>
            </a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-brush-fill" @click="selectTool('brush')"></i>
            </a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-eraser-fill" @click="selectTool('eraser')"></i>
            </a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-square" @click="selectTool('square')"></i>
            </a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-circle" @click="selectTool('circle')"></i>
            </a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-triangle" @click="selectTool('triangle')"></i>
            </a>
        </li>
        <li class="nav-item" @click="fullscreen">
            <a class="nav-link" href="#">
                <i class="bi bi-fullscreen"></i>
            </a>
        </li>
        <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button" aria-expanded="false">Size</a>
            <ul class="dropdown-menu bg-dark">
                <li v-for="i in 15" :key="i" @click="setSize(i)"><a class="dropdown-item text-white" href="#">{{ i }}</a></li>
            </ul>
        </li>
        <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button" aria-expanded="false">Color</a>
            <ul class="dropdown-menu bg-dark">
                <li><a class="dropdown-item text-white" href="#">Red</a></li>
                <li><a class="dropdown-item text-white" href="#">Blue</a></li>
                <li><a class="dropdown-item text-white" href="#">Yellow</a></li>
                <li><a class="dropdown-item text-white" href="#">White</a></li>
            </ul>
        </li>
        <li class="nav-item dropdown">
            <a class="nav-link dropdown-toggle" data-bs-toggle="dropdown" href="#" role="button" aria-expanded="false">Fill color</a>
            <ul class="dropdown-menu bg-dark">
                <li><a class="dropdown-item text-white" href="#" @click="fillColor(true)">enable</a></li>
                <li><a class="dropdown-item text-white" href="#" @click="fillColor(false)">disable</a></li>
            </ul>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-file-minus" @click="selectTool('clear')"></i>
            </a>
        </li>
        <li class="nav-item">
            <a class="nav-link" href="#">
                <i class="bi bi-box-arrow-down"></i>
            </a>
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
            document.querySelector("#board").style.width = "100%";
            document.querySelector("#board").style.height = "100%";
            if (this.isFull) {
                document.exitFullscreen();
            } else {
                document.body.requestFullscreen();
            }
            this.isFull = !this.isFull;
        },
        selectTool(tool) {
            this.$emit("selectTool", tool);
        },
        fillColor(is) {
            this.$emit("fillColor", is);
        },
        setSize(s) {
            this.$emit("changeSize", s);
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