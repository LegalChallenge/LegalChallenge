<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Legal Challenge - Il Quiz del Diritto</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f5f5f5;
            margin: 0;
            padding: 0;
            text-align: center;
        }

        #quiz-container {
            margin: 50px auto;
            padding: 20px;
            max-width: 800px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }

        h1 {
            color: #2C3E50;
        }

        .question {
            font-size: 1.5em;
            margin-bottom: 20px;
        }

        .answers button {
            display: block;
            width: 100%;
            margin: 10px 0;
            padding: 10px;
            font-size: 1.2em;
            background-color: #3498db;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .answers button:hover {
            background-color: #2980b9;
        }

        .hidden {
            display: none;
        }

        #timer {
            font-size: 1.2em;
            margin-bottom: 20px;
        }

        #score-board {
            font-size: 1.5em;
            margin-top: 20px;
        }

        img {
            width: 150px;
            margin: 20px 0;
        }
    </style>
</head>
<body>

    <div id="quiz-container">
        <h1>Legal Challenge - Il Quiz del Diritto</h1>
        <div id="timer">Tempo rimanente: <span id="time">30</span> secondi</div>
        
        <div id="question-container">
            <div class="question" id="question">Domanda 1</div>
            <div class="answers">
                <button onclick="checkAnswer(0)">Risposta 1</button>
                <button onclick="checkAnswer(1)">Risposta 2</button>
                <button onclick="checkAnswer(2)">Risposta 3</button>
                <button onclick="checkAnswer(3)">Risposta 4</button>
            </div>
        </div>

        <div id="score-board" class="hidden">
            <h2>Punteggio Totale: <span id="score">0</span></h2>
            <button onclick="restartQuiz()">Ricomincia il Quiz</button>
        </div>

        <img id="image" src="https://via.placeholder.com/150" alt="Immagine legale" />
    </div>

    <script>
        const questions = [
            {
                question: "Cosa succede se non rispetti il regolamento scolastico?",
                answers: ["Niente, è solo una linea guida", "Potresti ricevere un richiamo o una sanzione disciplinare", "La scuola non può fare nulla", "Potresti essere espulso immediatamente"],
                correct: 1,
                image: "https://via.placeholder.com/150/0000FF"
            },
            {
                question: "Qual è il diritto principale di uno studente a scuola?",
                answers: ["Il diritto al gioco", "Il diritto allo studio", "Il diritto di non seguire le lezioni", "Il diritto di non fare i compiti"],
                correct: 1,
                image: "https://via.placeholder.com/150/00FF00"
            },
            // Aggiungi le altre 8 domande qui nello stesso formato...
        ];

        let currentQuestion = 0;
        let score = 0;
        let timeLeft = 30;
        let timer;

        function loadQuestion() {
            document.getElementById('question').textContent = questions[currentQuestion].question;
            const buttons = document.querySelectorAll('.answers button');
            buttons.forEach((button, index) => {
                button.textContent = questions[currentQuestion].answers[index];
            });
            document.getElementById('image').src = questions[currentQuestion].image;
            timeLeft = 30;
            startTimer();
        }

        function startTimer() {
            clearInterval(timer);
            timer = setInterval(() => {
                timeLeft--;
                document.getElementById('time').textContent = timeLeft;
                if (timeLeft <= 0) {
                    clearInterval(timer);
                    checkAnswer(-1); // Nessuna risposta
                }
            }, 1000);
        }

        function checkAnswer(selectedAnswer) {
            clearInterval(timer);
            if (selectedAnswer === questions[currentQuestion].correct) {
                score += 10; // Assegna 10 punti per risposta corretta
            }

            currentQuestion++;
            if (currentQuestion < questions.length) {
                loadQuestion();
            } else {
                endQuiz();
            }
        }

        function endQuiz() {
            document.getElementById('question-container').classList.add('hidden');
            document.getElementById('score-board').classList.remove('hidden');
            document.getElementById('score').textContent = score;
        }

        function restartQuiz() {
            score = 0;
            currentQuestion = 0;
            document.getElementById('score-board').classList.add('hidden');
            document.getElementById('question-container').classList.remove('hidden');
            loadQuestion();
        }

        window.onload = loadQuestion;
    </script>

</body>
</html>
