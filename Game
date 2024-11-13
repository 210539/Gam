<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flappy Bird Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="game-container">
        <div class="bird" id="bird"></div>
        <div id="score">Score: 0</div>
    </div>
    <script src="script.js"></script>
</body>
</html>/* style.css */
body {
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #70c5ce;
}

.game-container {
    position: relative;
    width: 320px;
    height: 480px;
    background-color: #87CEEB;
    overflow: hidden;
    border: 2px solid #000;
}

.bird {
    position: absolute;
    width: 30px;
    height: 30px;
    background-color: yellow;
    border-radius: 50%;
    top: 50%;
    left: 50px;
}

.pipe {
    position: absolute;
    width: 60px;
    background-color: #228B22;
    top: 0;
}

.pipe-top {
    height: 50%;
    border-bottom: 5px solid #000;
}

.pipe-bottom {
    height: 50%;
    border-top: 5px solid #000;
}

#score {
    position: absolute;
    top: 10px;
    left: 10px;
    font-size: 20px;
    color: #fff;
}// script.js

const bird = document.getElementById('bird');
const gameContainer = document.querySelector('.game-container');
const scoreDisplay = document.getElementById('score');

let birdY = 200;  // Initial vertical position
let gravity = 2;  // Gravity to pull bird down
let isGameOver = false;
let score = 0;

// Control bird jump
function jump() {
    if (!isGameOver) birdY -= 40;
}

// Key event for jump
document.addEventListener('keydown', jump);

// Game loop
function gameLoop() {
    if (isGameOver) return;

    // Apply gravity
    birdY += gravity;
    bird.style.top = birdY + 'px';

    // Generate pipes
    generatePipes();

    // Check for collisions
    if (checkCollisions()) {
        gameOver();
    } else {
        score++;
        scoreDisplay.textContent = 'Score: ' + Math.floor(score / 100);
    }

    requestAnimationFrame(gameLoop);
}

// Function to generate pipes
function generatePipes() {
    const pipes = document.querySelectorAll('.pipe');

    // Move existing pipes
    pipes.forEach(pipe => {
        const pipeX = parseInt(window.getComputedStyle(pipe).getPropertyValue('left'));
        if (pipeX < -60) {
            pipe.remove();  // Remove off-screen pipes
        } else {
            pipe.style.left = pipeX - 2 + 'px';
        }
    });

    // Generate new pipes
    if (Math.random() < 0.02) {
        createPipePair();
    }
}

// Create a pair of pipes (top and bottom)
function createPipePair() {
    const gap = 120;
    const pipeHeight = Math.floor(Math.random() * (gameContainer.clientHeight - gap));
    
    // Top pipe
    const pipeTop = document.createElement('div');
    pipeTop.classList.add('pipe', 'pipe-top');
    pipeTop.style.height = pipeHeight + 'px';
    pipeTop.style.left = '320px';
    gameContainer.appendChild(pipeTop);

    // Bottom pipe
    const pipeBottom = document.createElement('div');
    pipeBottom.classList.add('pipe', 'pipe-bottom');
    pipeBottom.style.height = gameContainer.clientHeight - pipeHeight - gap + 'px';
    pipeBottom.style.top = pipeHeight + gap + 'px';
    pipeBottom.style.left = '320px';
    gameContainer.appendChild(pipeBottom);
}

// Check for collisions
function checkCollisions() {
    const birdRect = bird.getBoundingClientRect();
    const pipes = document.querySelectorAll('.pipe');

    // Collision with pipes or screen bounds
    for (let pipe of pipes) {
        const pipeRect = pipe.getBoundingClientRect();
        if (
            birdRect.left < pipeRect.left + pipeRect.width &&
            birdRect.left + birdRect.width > pipeRect.left &&
            birdRect.top < pipeRect.top + pipeRect.height &&
            birdRect.top + birdRect.height > pipeRect.top
        ) {
            return true;
        }
    }

    // Collision with top or bottom bounds of game container
    if (birdY <= 0 || birdY + bird.clientHeight >= gameContainer.clientHeight) {
        return true;
    }

    return false;
}

// End game
function gameOver() {
    isGameOver = true;
    alert('Game Over! Your score: ' + Math.floor(score / 100));
    location.reload();
}

// Start game loop
gameLoop();
