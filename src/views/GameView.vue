<template>
    <GameBoard :board_size="getNumber(this.$route.params.board_size)" />
</template>

<script>
import GameBoard from "../components/GameBoard.vue"

const DEFAULT_VALUE = 10

export default {
    name: "GameView",
    components: {
        GameBoard,
    },
    methods: {
        getNumber(num) {
            if (isNaN(Number(num)) || num < 2) {
                return DEFAULT_VALUE
            }
            return Number(num)
        }
    }
}
</script>