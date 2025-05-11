# Guessing_Game
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>GuessMaster: Number Guessing Game</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="game-container">
        <h1>🔢 GuessMaster</h1>
        <p>Guess a number between 1 and 100!</p>
        <input type="number" id="guessInput" min="1" max="100">
        <button id="submitGuess">Submit</button>
        <p id="hint"></p>
        <p id="attempts">Attempts left: 10</p>
        <button id="restart">Play Again</button>
    </div>
    <script src="script.js"></script>
</body>
</html>




CSS


body {
    font-family: 'Arial', sans-serif;
    text-align: center;
    background: #f0f8ff;
    margin: 0;
    padding: 20px;
}

.game-container {
    background: white;
    border-radius: 10px;
    padding: 20px;
    max-width: 400px;
    margin: 0 auto;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

input {
    padding: 10px;
    margin: 10px 0;
    width: 80%;
}

button {
    padding: 10px 20px;
    background: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

button:hover {
    background: #45a049;
}

#hint {
    font-weight: bold;
    color: #d9534f;
}

#attempts {
    color: #5bc0de;
}





JAVASCRIPT

let secretNumber = Math.floor(Math.random() * 100) + 1;
let attemptsLeft = 10;

document.getElementById('submitGuess').addEventListener('click', checkGuess);
document.getElementById('restart').addEventListener('click', restartGame);

function checkGuess() {
    const guess = parseInt(document.getElementById('guessInput').value);
    const hintElement = document.getElementById('hint');
    const attemptsElement = document.getElementById('attempts');

    if (isNaN(guess) || guess < 1 || guess > 100) {
        hintElement.textContent = "Please enter a valid number (1-100)!";
        return;
    }

    attemptsLeft--;
    attemptsElement.textContent = `Attempts left: ${attemptsLeft}`;

    if (guess === secretNumber) {
        hintElement.textContent = "🎉 Correct! You win!";
        document.body.style.backgroundColor = "#d4edda";
        disableInput();
    } else if (attemptsLeft === 0) {
        hintElement.textContent = `Game Over! The number was ${secretNumber}.`;
        disableInput();
    } else {
        hintElement.textContent = guess > secretNumber ? "📉 Too high!" : "📈 Too low!";
    }
}

function disableInput() {
    document.getElementById('guessInput').disabled = true;
    document.getElementById('submitGuess').disabled = true;
}

function restartGame() {
    secretNumber = Math.floor(Math.random() * 100) + 1;
    attemptsLeft = 10;
    document.getElementById('hint').textContent = "";
    document.getElementById('attempts').textContent = `Attempts left: ${attemptsLeft}`;
    document.getElementById('guessInput').value = "";
    document.getElementById('guessInput').disabled = false;
    document.getElementById('submitGuess').disabled = false;
    document.body.style.backgroundColor = "#f0f8ff";
}
