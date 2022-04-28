<template>
    <div v-if="tileState !== 'dotted'" class="tile" :class="tileState"
        v-on:click.right.prevent="handleRightClick"
        v-on:click.left="handleLeftClick"
    >
        <span v-if="numbered" class="number">
            {{ islandSize || 0 }}
        </span>
    </div>
    <div v-else-if="tileState === 'dotted'" class="tile" :class="tileState"
        v-on:click.right.prevent="handleRightClick"
        v-on:click.left="handleLeftClick"
    >
        <img src="/images/black_dot.png" alt="dot">
    </div>
</template>

<script>
export default {
    name: 'Tile',
    props: ['onStateChange', 'pos', 'islandSize'],

    data() {
        return {
            tileState: 'white',
            numbered: false,
        };
    },

    methods: {
        handleLeftClick() {
            if (this.numbered)
                return;

            if (this.tileState === 'black')
                this.tileState = 'white';
            else
                this.tileState = 'black';

            this.onStateChange(this.pos, this.tileState);
        },
        handleRightClick() {
            if (this.numbered)
                return;

            if (this.tileState === 'dotted')
                this.tileState = 'white';
            else
                this.tileState = 'dotted';

            this.onStateChange(this.pos, this.tileState);
        },
    }
}
</script>

<style scoped>
    .tile {
        box-sizing: border-box;
        text-align: center;
        width: 25px;
        height: 25px;

        border-top: solid black 1px;
        border-left: solid black 1px;
    }

    .tile:last-child {
        border-right: solid black 1px;
        /* border-top: solid black 1px;*/
    }

    .black {
        background-color: black;
    }

    .dotted > img {
        width: 99.9%;
        height: 99.9%;
        user-select: none;
    }

    .number {
        user-select: none;
        vertical-align: middle;
    }
</style>
