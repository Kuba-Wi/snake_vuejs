<template>
    <div>
        <p>Game over. Your score: {{score}}</p>
        <input type="button" @click="goHome" value="End">
    </div>
</template>

<script>
export default {
    props: {
        score: Number
    },
    methods: {
        goHome() {
            this.$router.push("/")
        }
    }
}
</script>

<style scoped>
div {
    position: absolute;
    top: 20%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 20px;
    font-weight: bold;
    background-color: lightgray;
    padding: 10px;
    border-radius: .3em;
    border: 2px solid black;
}

p {
    color: black;
    width: 300px;
}

input {
    height: 50px;
    width: 100px;
    color: black;
    background-color: white;
    border: 2px solid black;
    border-radius: .3em;
    font-size: 20px;
    font-weight: bold;
}

input:hover {
    background-color: gray;
}
</style>
