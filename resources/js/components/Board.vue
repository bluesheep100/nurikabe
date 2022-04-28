<template>
    <div class="grid" :style="{ 'grid-template-rows': `repeat(${boardMap.length}, 25px)` }">
        <div class="grid row" :style="{ 'grid-template-columns': `repeat(${row.length}, 25px)`}" v-for="(row, i) in boardMap" :key="i">
            <Tile v-for="(col, j) in row" :key="j" v-bind="col" :onStateChange="onStateChange"/>
        </div>
    </div>
</template>

<script>
import Tile from './Tile';

export default {
    props: ['boardMap'],
    components: { Tile },
    data() {
        return {
        };
    },
    name: 'Board',

    methods: {
        onStateChange(tilePos, newState) {

            console.log(tilePos, newState);
        }
    }
}
</script>

<style scoped>
    .grid {
        display: grid;
    }

    .row:last-child {
        border-bottom: solid black 1px;
    }
</style>
