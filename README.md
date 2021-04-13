# JOGO-DA-COBRINHA

TODOS COD:

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="./style.css">
    <script defer src="./script.js"></script>
    <title>Snake Game</title>
</head>
<body>
    <h1>Snake Game</h1>
    
    <canvas id="snake" width="512" height="512"></canvas>
</body>
</html>

--------------------------------------------------------------------------------------------------------------------------------------

let canvas = document.getElementById("snake");
let context = canvas.getContext("2d");
let box = 32;
let snake = [];
snake[0] = {
    x: 8 * box,
    y: 8 * box
};
let direction = "right"
let food = {
    x: Math.floor(Math.random() * 15  + 1) * box,
    y: Math.floor(Math.random() * 15 + 1) * box
}

function criarBG(){
    context.fillStyle = "lightgreen";
    context.fillRect(0, 0, 16*box, 16*box);    
}

function snakeCreate() {
    for (let index = 0; index < snake.length; index++) {
        context.fillStyle = "green";
        context.fillRect(snake[index].x, snake[index].y, box, box);    
    }
}

function drawFood(){
    context.fillStyle = "red";
    context.fillRect(food.x, food.y, box, box)
}

document.addEventListener('keydown', update);

function update(event) {
    if (event.keyCode == 37 && direction != "right")  direction = "left"
    if (event.keyCode == 38 && direction != "down") direction = "up";
    if (event.keyCode == 39 && direction != "left") direction = "right";
    if (event.keyCode == 40 && direction != "up") direction = "down";
}

function iniciarJogo() {
    if (snake[0].x > 15 * box && direction == "right") snake[0].x = 0;
    if (snake[0].x < 0 && direction == "left") snake[0].x = 16 * box;
    if (snake[0].y > 15 * box && direction == "down") snake[0].y = 0;
    if (snake[0].y < 0 && direction == "up") snake[0].y = 16 * box;
    
    for (let index = 1; index < snake.length; index++) {
        if (snake[0].x == snake[index].x && snake[0].y == snake[index].y)
            clearInterval(jogo);
            alert('Game Over :(');            
        }
    }

    criarBG();
    snakeCreate();
    drawFood();

    let snakeX = snake[0].x;
    let snakeY = snake[0].y;

    if (direction == "right") snakeX += box;
    if (direction == "left") snakeX -= box;
    if (direction == "up") snakeY -=box;
    if (direction == "down") snakeY +=box;

    if (snakeX != food.x || snakeY != food.y) {
        snake.pop();
    } else {
        food.x = Math.floor(Math.random() * 15  + 1) * box;
        food.y = Math.floor(Math.random() * 15 + 1) * box
    }

    let newHead = {
        x: snakeX,
        y: snakeY
    }

    snake.unshift(newHead);
    


let jogo = setInterval(iniciarJogo, 100)




-------------------------------------------------------------
