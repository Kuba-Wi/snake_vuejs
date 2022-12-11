<template>
    <div id="main">
        <input id=btn type="button" value="Start game" @click="start_game">
        <div>
            <p>Set board size:</p>
            <input id="size_input" type="text" v-model="board_size">
        </div>
    </div>
</template>

<script>
export default {
    name: "HomeView",
    data() {
        return {
            board_size: 10
        }
    },
    methods: {
        start_game() {
            this.$router.push({name: 'game', params: {board_size: this.board_size}})
        }
    }
}
</script>

<style scoped>
#main {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: lightgray;
    padding: 200px;
    border-radius: .3em;
}
#btn {
    height: 80px;
    width: 200px;
    margin-bottom: 20px;
    color: black;
    background-color: rgb(243, 243, 165);
    border: 2px solid black;
    border-radius: .3em;
    font-weight: bold;
    font-size: 25px;
}

#btn:hover {
    background-color: #2D9CDB;
}

p {
    display: inline;
    margin-right: 10px;
    font-size: 20px;
}

#size_input {
    width: 3ch;
    font-size: 20px;
}
</style>
