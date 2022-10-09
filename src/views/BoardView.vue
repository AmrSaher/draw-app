<template>
    <div class="board bg-dark">
        <DrawNav @selectTool="selectTool" @fillColor="fillColor" @changeSize="changeSize" />
        <Canvas :tool="selectedTool" :fillColor="isFill" :size="size" />
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
            selectedTool: "brush",
            isFill: false,
            size: 5
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
}
</style>