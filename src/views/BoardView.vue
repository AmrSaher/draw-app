<template>
    <div class="board bg-dark">
        <DrawNav @selectTool="selectTool" @fillColor="fillColor" @changeSize="changeSize" @color="selectColor" @changeWindowSize="resizeWindow" />
        <Canvas :tool="selectedTool" :fillColor="isFill" :size="size" :color="color" :full="full" />
    </div>
</template>

<script>
import DrawNav from '../components/DrawNav.vue';
import Canvas from '../components/Canvas.vue';

export default {
    name: "BoardView",
    components: {
        DrawNav,
        Canvas
    },
    data() {
        return {
            selectedTool: "mouse",
            isFill: false,
            size: 5,
            color: "yellow",
            full: 1
        };
    },
    methods: {
        selectTool(tool) {
            this.selectedTool = tool;
        },
        fillColor(is) {
            this.isFill = is;
        },
        changeSize(s) {
            this.size = s;
        },
        selectColor(c) {
            this.color = c;
        },
        resizeWindow() {
            this.full += 1
        }
    }
};
</script>

<style lang="scss" scoped>
.board {
    width: 100vw;
    height: 100vh;
    max-width: 100vw;
    max-height: 100vh;
    padding: 0;
}
</style>