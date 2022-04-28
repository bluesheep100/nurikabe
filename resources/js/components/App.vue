<template>
    <div>
        <div class="container">
            <form class="new-board-form" v-on:submit.prevent="generateBoard">
                <label for="width">Width</label>
                <input type="number" name="width" id="width" v-model.number="width">

                <label for="height">Height</label>
                <input type="number" name="height" id="height" v-model.number="height">

                <button class="btn" type="submit">Generate</button>
            </form>

        </div>
        <div class="container">
            <Board v-if="showBoard" :board-map="boardMap"/>
        </div>
    </div>
</template>

<script>
import { Chance } from 'chance';
import Board from './Board';

export default {
    components: { Board },
    name: 'App',
    data() {
        return {
            width: 5,
            height: 5,
            showBoard: false,
            boardMap: [],
        };
    },

    mounted() {
    },

    methods: {
        generateBoard() {
            if (!this.validateForm())
                return;

            console.log(this.width);
            console.log(this.height);

            let boardMap = [];

            let chance = new Chance();
            let percent = chance.integer({min: 1, max: 100});
            let rowData = [];

            for (let row = 0; row < this.height; row++) {
                for (let col = 0; col < this.width; col++) {
                    console.log(col);
                    let numbered = percent <= 10;
                    rowData.push({
                        pos: {x: col, y: row},
                        numbered, // 10% chance to have a number
                        islandSize: numbered ? chance.integer({min: 1, max: 3}) : 0,
                    });
                }

                boardMap.push(rowData);
                rowData = [];
            }

            this.boardMap = boardMap;
            console.log(this.boardMap);
            this.showBoard = true;
        },
        validateForm() {
            return this.width > 0 && this.height > 0;
        },
    },
}
</script>

<style scoped>
    .container {
        max-width: min-content;
        margin: 0 auto;
    }

    .new-board-form {
        margin-bottom: 1rem;
    }

    .new-board-form input {
        border-radius: 5px;
        border-color: rgba(0,0,0, 0.3);
        outline: none;
        margin-bottom: .5rem;
    }

    .btn {
        width: 100%;
        outline: none;
        border: none;
        padding: 8px 0;

        color: whitesmoke;
        background-color: #359369;
        border-radius: 5px;
    }

    .btn:hover {
        background-color: #297d57;
    }
</style>
