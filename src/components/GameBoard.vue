<template>
    <div id="board">
        <EndGame v-if="game_over" :score="score" />
    </div>
</template>

<script>
import { Snake, direction } from "../classes/snake.js";
import { Food } from "../classes/food.js"

import EndGame from "../components/EndGame.vue"

export default {
    name: "GameBoard",
    props: {
        board_size: Number
    },
    data() {
        return {
            snake: new Snake(this.board_size),
            food: new Food(this.board_size),
            board: null,
            frame_count: 0,
            new_direction: 0,
            score: 0,
            game_over: false
        }
    },
    components: {
        EndGame
    },
    mounted: function() {
        this.board = document.getElementById("board")
        document.documentElement.style.setProperty("--columns-row", this.board_size)
        this.board.style.width = `${this.board_size * 40}px`
        this.board.style.height = `${this.board_size * 40}px`

        this.listen_arrow_presses()
        this.start_game()
    },
    methods: {
        start_game() {
            this.button_visible = false
            this.set_food_position()
            this.refresh_board()
            window.requestAnimationFrame(this.game_loop)
        },
        reset_game() {
            this.clear_board()
            this.score = this.snake.get_body_length()
            this.game_over = true
        },
        game_loop() {
            ++this.frame_count
            if (this.frame_count >= 10) {
                this.snake.change_move_direction(this.new_direction)
                this.snake.move()
                if (this.snake.is_snake_collision()) {
                    this.reset_game()
                    return
                }
                else if (this.snake.is_snake_position(this.food.x, this.food.y)) {
                    this.snake.add_body()
                    this.set_food_position()
                }
                this.refresh_board()
                this.frame_count = 0
            }

            window.requestAnimationFrame(this.game_loop)
        },
        clear_board() {
            var divs = this.board.getElementsByTagName("div")
            while (divs.length > 0) {
                divs[0].remove()
            }
        },
        refresh_board() {
            this.clear_board()
            this.snake.draw(this.board)
            this.food.draw(this.board)
        },
        set_food_position() {
            while (this.snake.is_snake_position(this.food.x, this.food.y)) {
                this.food.set_new_position()
            }
        },
        listen_arrow_presses() {
            document.addEventListener("keydown", (event) => {
                switch (event.key) {
                    case "ArrowUp":
                        this.new_direction = direction.up
                        break;
                    case "ArrowRight":
                        this.new_direction = direction.right
                        break;
                    case "ArrowDown":
                        this.new_direction = direction.down
                        break;
                    case "ArrowLeft":
                        this.new_direction = direction.left
                        break;
                }
            })
        }
    }
}
</script>

<style>
:root {
    --columns-row: 1;
}
#board {
    background-color: rgb(126, 245, 136);
    border: .25vmin solid black;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: grid;
    grid-template-rows: repeat(var(--columns-row), 1fr);
    grid-template-columns: repeat(var(--columns-row), 1fr);
}

.snake {
    background-color: blue;
    border: .25vmin solid black;
}

.food {
    background-color: yellow;
    border: .25vmin solid black;
}
</style>
