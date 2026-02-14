# ghazal
<!DOCTYPE html>
<html>
<head>
<title>Grade 1 Yousefi - Subtraction Game</title>

<style>
body {
    margin: 0;
    font-family: Comic Sans MS, cursive;
    text-align: center;
    background: linear-gradient(45deg, red, orange, yellow, green, blue, purple);
    background-size: 400% 400%;
    animation: rainbow 8s infinite alternate;
}

@keyframes rainbow {
    0% {background-position: left;}
    100% {background-position: right;}
}

h1 {
    background: white;
    display: inline-block;
    padding: 20px 40px;
    border-radius: 25px;
    margin-top: 30px;
    font-size: 38px;
    color: hotpink;
    box-shadow: 0 0 25px gold;
}

.game-box {
    background: white;
    margin: 30px auto;
    padding: 30px;
    width: 350px;
    border-radius: 20px;
    box-shadow: 0 0 20px black;
}

.question {
    font-size: 35px;
    margin: 20px;
}

input {
    font-size: 20px;
    padding: 5px;
    width: 80px;
    text-align: center;
}

button {
    font-size: 18px;
    padding: 10px 20px;
    margin-top: 10px;
    background: lightgreen;
    border: none;
    border-radius: 10px;
    cursor: pointer;
}

#result {
    font-size: 22px;
    margin-top: 15px;
}

#stars {
    font-size: 25px;
    margin-top: 10px;
    color: gold;
}

.options {
    margin-bottom: 15px;
    font-size: 16px;
}
</style>
</head>

<body>

<h1>🌈 Welcome to Grade 1 Yousefi 🌈</h1>

<div class="game-box">

    <div class="options">
        <label>
            <input type="checkbox" id="removeZero">
            Remove subtraction with 0
        </label>
    </div>

    <div class="question" id="question"></div>

    <input type="number" id="answer">
    <br>
    <button onclick="checkAnswer()">Submit</button>

    <div id="result"></div>
    <div id="stars">⭐ Stars: 0</div>

</div>

<script>
let stars = 0;
let usedQuestions = [];
let currentAnswer = 0;

function generateQuestion() {

    if (usedQuestions.length >= 50) {
        document.getElementById("question").innerHTML = "🎉 You Finished All Questions! 🎉";
        return;
    }

    let num1, num2, questionText;
    let removeZero = document.getElementById("removeZero").checked;

    do {
        num1 = Math.floor(Math.random() * 10) + 1;
        num2 = Math.floor(Math.random() * (num1 + 1));

        if (removeZero && num2 === 0) {
            continue;
        }

        questionText = num1 + " - " + num2;

    } while (usedQuestions.includes(questionText) || (removeZero && num2 === 0));

    usedQuestions.push(questionText);

    currentAnswer = num1 - num2;
    document.getElementById("question").innerHTML = questionText;
    document.getElementById("answer").value = "";
}

function checkAnswer() {

    let userAnswer = parseInt(document.getElementById("answer").value);

    if (userAnswer === currentAnswer) {
        stars++;
        document.getElementById("result").innerHTML = "😊 Correct! Great Job!";
        document.getElementById("stars").innerHTML = "⭐ Stars: " + stars;
        generateQuestion();
    } else {
        document.getElementById("result").innerHTML = "❌ Try Again! 😢";
    }
}

generateQuestion();
</script>

</body>
</html>
