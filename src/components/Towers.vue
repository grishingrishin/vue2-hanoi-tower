<template>
    <ul class="towers">
        <div class="towers__body">
            <div class="towers__main" @dragover="dragOver" @dragleave="dragLeave">
                <div
                    :class="['towers__col', 'tower', { 'drag-and-drop': tower.length < 3 && isDraggedOver }]"
                    v-for="(tower, column) of towers"
                    :key="column"
                    @dragenter="dragEnter($event, column)"
                >
                    <ul class="tower__list">
                        <template v-for="(circle, index) of tower">
                            <li
                                class="tower__item"
                                :style="{ maxWidth: `${circle}00px` }"
                                :key="index"
                                @dragstart="dragStart($event, circle, column)"
                                @dragend="dragEnd"
                                draggable
                                v-if="index == 0"
                            ></li>
                            <li :style="{ maxWidth: `${circle}00px` }" class="tower__item" :key="index" v-else></li>
                        </template>
                    </ul>
                </div>
            </div>
        </div>
    </ul>
</template>

<script>
export default {
    name: 'Towers',
    data() {
        return {
            isDraggedOver: false,
            towers: [[1, 2, 3], [], []],
            size: 3,
            draggable: null,
            activeColumn: null,
            nextColumn: null,
        };
    },
    methods: {
        dragStart(e, circle, column) {
            this.draggable = circle;
            this.activeColumn = column;
        },
        dragEnter(e, column) {
            this.nextColumn = column;
        },
        dragOver() {
            this.isDraggedOver = true;
        },
        dragLeave() {
            this.isDraggedOver = false;
        },
        dragEnd() {
            const { nextColumn, towers, size } = this;
            const lengthOfTargetColumn = towers[nextColumn].length;

            if (lengthOfTargetColumn < size) {
                const { activeColumn, draggable } = this;
                this.towers[activeColumn].shift();
                this.towers[nextColumn].unshift(draggable);
            }

            return this.destroy();
        },
        destroy() {
            this.draggable = null;
            this.nextColumn = null;
            this.activeColumn = null;
        },
    },
};
</script>

<style>
.towers {
    display: flex;
    height: 100vh;
    align-items: center;
    justify-content: center;
}

.towers__body {
    display: flex;
    width: 100%;
    max-width: 1162px;
    min-height: 480px;
    margin: 0 auto;
    padding: 0 14px;
    align-items: center;
    justify-content: center;
}

.towers__main {
    display: flex;
    width: 100%;
    min-height: 182px;
    justify-content: space-around;
}

.tower {
    position: relative;
    z-index: 1;
    flex: 0 1 340px;
    margin: 4px;
}

.tower::before {
    content: '';
    position: absolute;
    top: 0;
    left: calc(50% - 8px);
    z-index: -1;
    width: 16px;
    height: 100%;
    background-color: #79553d;
}

.tower::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    z-index: -1;
    width: 100%;
    height: 16px;
    background-color: #79553d;
}

.tower__list {
    display: flex;
    height: 100%;
    padding: 22px 4px;
    flex-direction: column;
    align-items: center;
    justify-content: flex-end;
}

.tower__item {
    width: 100%;
    height: 18px;
    margin-top: 8px;
    background-color: #cd9575;
    border-radius: 2px;
}

.tower__item[draggable] {
    cursor: grabbing;
}
</style>
