# Jafari
quiz
Creating a simple quiz using HTML can be achieved with a combination of HTML for the structure and JavaScript for interactivity. Here's a basic example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        .quiz-container {
            max-width: 600px;
            margin: auto;
        }
        .question {
            margin-bottom: 10px;
        }
        .options {
            list-style-type: none;
            padding: 0;
        }
        .options li {
            margin-bottom: 5px;
        }
    </style>
</head>
<body>

<div class="quiz-container">
    <div class="question" id="question"></div>
    <ul class="options" id="options"></ul>
    <button onclick="checkAnswer()">Submit Answer</button>
    <p id="result"></p>
</div>

<script>
    const quizData = [
        {
            question: "What is the capital of France?",
            options: ["Berlin", "Madrid", "Paris", "Rome"],
            correctAnswer: "Paris"
        },
        {
            question: "Which planet is known as the Red Planet?",
            options: ["Mars", "Venus", "Jupiter", "Saturn"],
            correctAnswer: "Mars"
        }
        // Add more questions as needed
    ];

    let currentQuestion = 0;
    let score = 0;

    function loadQuestion() {
        const questionElement = document.getElementById("question");
        const optionsElement = document.getElementById("options");

        questionElement.textContent = quizData[currentQuestion].question;
        optionsElement.innerHTML = "";

        quizData[currentQuestion].options.forEach((option, index) => {
            const li = document.createElement("li");
            li.textContent = option;
            li.setAttribute("data-index", index);
            optionsElement.appendChild(li);
        });
    }

    function checkAnswer() {
        const selectedOption = document.querySelector("li.selected");
        const resultElement = document.getElementById("result");

        if (selectedOption) {
            const selectedIndex = selectedOption.getAttribute("data-index");
            const correctAnswer = quizData[currentQuestion].correctAnswer;

            if (quizData[currentQuestion].options[selectedIndex] === correctAnswer) {
                score++;
                resultElement.textContent = "Correct!";
            } else {
                resultElement.textContent = `Incorrect! The correct answer is ${correctAnswer}.`;
            }

            // Move to the next question or finish the quiz
            currentQuestion++;
            if (currentQuestion < quizData.length) {
                loadQuestion();
            } else {
                resultElement.textContent = `Quiz completed. Your score: ${score}/${quizData.length}`;
            }
        } else {
            resultElement.textContent = "Please select an answer.";
        }
    }

    document.getElementById("options").addEventListener("click", function (event) {
        const selectedOption = event.target;

        if (selectedOption.tagName === "LI") {
            // Deselect all options
            const options = document.querySelectorAll("li");
            options.forEach(option => option.classList.remove("selected"));

            // Select the clicked option
            selectedOption.classList.add("selected");
        }
    });

    // Initial load
    loadQuestion();
</script>

</body>
</html>
```

This code provides a simple structure for a quiz with two questions. You can extend the `quizData` array with additional questions, options, and correct answers as needed. The code uses vanilla JavaScript for simplicity, but you can explore libraries like jQuery or frameworks like React for more sophisticated applications.