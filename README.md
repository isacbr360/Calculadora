/* HTML */

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora Interativa</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <script src="script.js"></script>
    <div class="calculator">
        <input type="text" id="display" class="display" disabled>
        <div class="buttons">
            <button class="btn" onclick="appendNumber('7')">7</button>
            <button class="btn" onclick="appendNumber('8')">8</button>
            <button class="btn" onclick="appendNumber('9')">9</button>
            <button class="btn" onclick="chooseOperation('+')">+</button>
            <button class="btn" onclick="appendNumber('4')">4</button>
            <button class="btn" onclick="appendNumber('5')">5</button>
            <button class="btn" onclick="appendNumber('6')">6</button>
            <button class="btn" onclick="chooseOperation('-')">-</button>
            <button class="btn" onclick="appendNumber('1')">1</button>
            <button class="btn" onclick="appendNumber('2')">2</button>
            <button class="btn" onclick="appendNumber('3')">3</button>
            <button class="btn" onclick="chooseOperation('')"></button>
            <button class="btn" onclick="appendNumber('0')">0</button>
            <button class="btn" onclick="clearDisplay()">C</button>
            <button class="btn" onclick="calculate()">=</button>
            <button class="btn" onclick="chooseOperation('/')">/</button>
        </div>
    </div>
</body>
</html>

/* CSS */

@charset "UTF-8";

body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f4f4f9;
}

.calculator {
    background-color: white;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    padding: 20px;
    width: 280px;
    text-align: center;
}

.display {
    width: 100%;
    height: 50px;
    font-size: 2rem;
    text-align: right;
    border: 1px solid #ccc;
    padding: 10px;
    margin-bottom: 20px;
    background-color: #f9f9f9;
    border-radius: 5px;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

.btn {
    background-color: #f0f0f0;
    border: 1px solid #ccc;
    padding: 20px;
    font-size: 1.5rem;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.2s;
}

.btn:hover {
    background-color: #e0e0e0;
}

.btn:active {
    background-color: #ccc;
}

/* JavaScript */

let currentInput = '';
let operation = null;
let previousInput = '';

const display = document.getElementById('display');

function appendNumber(number) {
    currentInput += number;
    display.value = currentInput;
}

function chooseOperation(op) {
    if (currentInput === '') return;
    if (previousInput !== '') {
        calculate();
    }
    operation = op;
    previousInput = currentInput;
    currentInput = '';
}

function clearDisplay() {
    currentInput = '';
    previousInput = '';
    operation = null;
    display.value = '';
}

function calculate() {
    let result;
    const prev = parseFloat(previousInput);
    const current = parseFloat(currentInput);

    if (isNaN(prev) || isNaN(current)) return;

    switch (operation) {
        case '+':
            result = prev + current;
            break;
        case '-':
            result = prev - current;
            break;
        case '*':
            result = prev * current;
            break;
        case '/':
            if (current === 0) {
                result = 'Erro';
            } else {
                result = prev / current;
            }
            break;
        default:
            return;
    }

    currentInput = result.toString();
    operation = null;
    previousInput = '';
    display.value = currentInput;
}
