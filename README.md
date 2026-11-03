# Rosa-lili03.gtihub.io
[My First Ever Site.html](https://github.com/user-attachments/files/34342689/My.First.Ever.Site.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>TIVIA TIME</title>
<style>
:root {
    color-scheme: dark;
    font-family: system-ui, -apple-system, Segoe UI, sans-serif;
    background: #100d18;
    color: #f8f2ff;
}
* { box-sizing: border-box; }
body {
    min-height: 100vh;
    margin: 0;
    padding: 24px;
    display: grid;
    place-items: center;
    background:
        radial-gradient(ellipse at 15% 10%, #482667 0, transparent 38%),
        radial-gradient(ellipse at 90% 85%, #26336b 0, transparent 35%),
        #100d18;
}
.card {
    width: min(100%, 700px);
    padding: clamp(22px, 5vw, 42px);
    border: 1px solid #55406c;
    border-radius: 24px;
    background: rgb(25 20 35 / 94%);
    box-shadow: 0 24px 80px #0008;
}
.kicker {
    color: #d3a8ff;
    font-size: .75rem;
    font-weight: 800;
    letter-spacing: .2em;
    text-transform: uppercase;
}
h1 { margin: 10px 0; font-size: clamp(2rem, 7vw, 3.2rem); }
p { color: #c9bdd6; line-height: 1.65; }
button, .button-link {
    display: inline-block;
    padding: 12px 18px;
    border: 1px solid #9662bd;
    border-radius: 11px;
    background: linear-gradient(110deg, #7139a5, #9a55bf);
    color: white;
    font: inherit;
    font-weight: 750;
    text-decoration: none;
    cursor: pointer;
}
button:hover, .button-link:hover { filter: brightness(1.15); }
button:focus-visible, a:focus-visible {
    outline: 3px solid #f3d9ff;
    outline-offset: 3px;
}
button:disabled { opacity: .6; cursor: wait; }
.hidden { display: none !important; }
.topline {
    display: flex;
    justify-content: space-between;
    gap: 12px;
    color: #ddc5f5;
    font-weight: 700;
}
.progress {
    height: 9px;
    margin: 16px 0 26px;
    overflow: hidden;
    border-radius: 99px;
    background: #34283f;
}
#progress-bar {
    width: 0;
    height: 100%;
    border-radius: inherit;
    background: linear-gradient(90deg, #a85cff, #f1a8e8);
    transition: width .3s ease;
}
#question { margin: 20px 0; font-size: clamp(1.25rem, 4vw, 1.7rem); }
#answers { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.answer {
    min-height: 58px;
    border-color: #574568;
    background: #211a2c;
    text-align: left;
}
.answer:hover:not(:disabled) { background: #39284d; }
#feedback { min-height: 28px; margin: 16px 0 0; font-weight: 700; }
.good { color: #8fe6b0; }
.bad { color: #ff9aaf; }
#game-card { max-width: 760px; }
#playfield {
    position: relative;
    height: min(48vh, 360px);
    min-height: 230px;
    margin: 18px 0;
    overflow: hidden;
    border: 2px solid #725391;
    border-radius: 16px;
    background:
        radial-gradient(circle at 30% 30%, #362348, transparent 42%),
        linear-gradient(135deg, #171327, #211831);
    touch-action: manipulation;
}
#star {
    position: absolute;
    left: 20px;
    top: 20px;
    width: 54px;
    height: 54px;
    padding: 0;
    border: 2px solid #ffe38c;
    border-radius: 50%;
    background: #ffbd38;
    color: #341d00;
    font-size: 1.8rem;
    line-height: 1;
    box-shadow: 0 0 22px #ffc642a8;
    user-select: none;
    will-change: left, top;
}
.game-stats {
    display: flex;
    justify-content: space-between;
    gap: 12px;
    font-weight: 750;
}
#result { text-align: center; }
.score {
    margin: 24px 0;
    padding: 18px;
    border: 1px solid #684b82;
    border-radius: 14px;
    background: #241a31;
    color: #e3c2ff;
    font-size: 1.4rem;
    font-weight: 800;
}
#funny-picture {
    width: min(100%, 420px);
    margin: 18px auto;
    padding: 12px;
    border: 1px solid #574568;
    border-radius: 16px;
    background: #171320;
}
#funny-picture svg { display: block; width: 100%; height: auto; }
.small-note { color: #a99bb8; font-size: .9rem; }
@media (max-width: 520px) {
    body { padding: 14px; }
    #answers { grid-template-columns: 1fr; }
    #playfield { height: 300px; }
}
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { scroll-behavior: auto !important; }
}
</style>
</head>
<body>

<main class="card" id="cover">
    <div class="kicker">✦ Be Readyy. Why Hellooo. ✦</div>
    <h1>Trivia Quest</h1>
    <p>
        Test your general knowledge! Get a question wrong and take on
        the speedy Star Dash to earn another try.
    </p>
    <button id="start-button" type="button">Start the quiz</button>
</main>

<section class="card hidden" id="quiz" aria-labelledby="question">
    <div class="kicker">Curiosity Quest</div>
    <div class="topline">
        <span id="question-number">Question 1 of 10</span>
        <span id="score-display">Score: 0</span>
    </div>
    <div class="progress" aria-label="Quiz progress">
        <div id="progress-bar"></div>
    </div>
    <h2 id="question"></h2>
    <div id="answers"></div>
    <p id="feedback" aria-live="polite"></p>
</section>

<section class="card hidden" id="game-card" aria-labelledby="game-title">
    <div class="kicker">Wrong answer — bonus challenge!</div>
    <h1 id="game-title">Star Dash ⭐</h1>
    <p>Catch <strong>3 stars</strong> before the timer reaches zero. They move fast!</p>
    <div class="game-stats">
        <span id="stars-count">Stars: 0 / 3</span>
        <span id="timer">Time: 12</span>
    </div>
    <div id="playfield" aria-label="Star collection play area">
        <button id="star" type="button" aria-label="Collect the moving star">★</button>
    </div>
    <p id="game-message" aria-live="polite">Click or tap the moving star!</p>
    <button id="retry-game" class="hidden" type="button">Try the challenge again</button>
</section>

<section class="card hidden" id="result" aria-labelledby="result-title">
    <div class="kicker">Quest complete</div>
    <h1 id="result-title">You did it!</h1>
    <p>Thanks for testing your trivia skills.</p>
    <div class="score" id="final-score"></div>

    <button id="funny-button" type="button" aria-expanded="false">
        😂 Show me a funny picture
    </button>

    <div id="funny-picture" class="hidden">
        <svg viewBox="0 0 420 300" role="img" aria-labelledby="cat-title cat-desc"
             xmlns="http://www.w3.org/2000/svg">
            <title id="cat-title">A cat wearing sunglasses and a tiny crown</title>
            <desc id="cat-desc">A very serious-looking orange cat who has clearly won the quiz.</desc>
            <rect width="420" height="300" rx="18" fill="#241a31"/>
            <circle cx="210" cy="155" r="95" fill="#f3a64a"/>
            <path d="M140 95 126 36l59 38M280 95l14-59-59 38"
                  fill="#f3a64a" stroke="#f3a64a" stroke-width="12" stroke-linejoin="round"/>
            <path d="M143 142h62l-8 29h-46zm72 0h62l-8 29h-46z"
                  fill="#20172a" stroke="#f8e5ff" stroke-width="5" stroke-linejoin="round"/>
            <path d="M205 150h10" stroke="#f8e5ff" stroke-width="6"/>
            <path d="M199 189q11 10 22 0" fill="none" stroke="#6c342a" stroke-width="5" stroke-linecap="round"/>
            <path d="m194 179 16 6 16-6-16 17z" fill="#f07e96"/>
            <path d="M163 187 95 177m69 22-70 9m163-21 68-10m-69 22 70 9"
                  stroke="#f5e5d7" stroke-width="4" stroke-linecap="round"/>
            <path d="m177 49 12-25 20 17 20-17 13 25z"
                  fill="#ffd45c" stroke="#fff0a6" stroke-width="4" stroke-linejoin="round"/>
            <text x="210" y="278" text-anchor="middle" fill="#f3d9ff"
                  font-family="system-ui,sans-serif" font-size="21" font-weight="700">
                CEO of knowing random stuff
            </text>
        </svg>
    </div>

    <p class="small-note">Thanks for playing! You can close this tab whenever you’re ready.</p>
    <button id="play-again" type="button">Play again</button>
</section>

<script>
"use strict";

const questions = [
    {
        question: "What is the capital city of Kazakhstan?",
        answers: ["Almaty", "Astana", "Tashkent", "Bishkek"],
        correct: "Astana"
    },
    {
        question: "What is the chemical symbol for tungsten?",
        answers: ["Tn", "Tu", "W", "Ts"],
        correct: "W"
    },
    {
        question: "Which is the largest desert on Earth?",
        answers: ["Sahara Desert", "Arabian Desert", "Gobi Desert", "Antarctic Desert"],
        correct: "Antarctic Desert"
    },
    {
        question: "In what year did Constantinople fall to the Ottoman Empire?",
        answers: ["1204", "1453", "1492", "1517"],
        correct: "1453"
    },
    {
        question: "Which moon is the largest in our solar system?",
        answers: ["Titan", "Europa", "Ganymede", "Earth's Moon"],
        correct: "Ganymede"
    },
    {
        question: "Which ancient Greek philosopher wrote The Republic?",
        answers: ["Aristotle", "Socrates", "Plato", "Pythagoras"],
        correct: "Plato"
    },
    {
        question: "Which strait separates Asia from North America?",
        answers: ["Strait of Gibraltar", "Bering Strait", "Dover Strait", "Bosporus"],
        correct: "Bering Strait"
    },
    {
        question: "What is the currency of Switzerland?",
        answers: ["Euro", "Swiss franc", "Krone", "Lira"],
        correct: "Swiss franc"
    },
    {
        question: "The chemical symbol Fe stands for which element?",
        answers: ["Fluorine", "Iron", "Francium", "Fermium"],
        correct: "Iron"
    },
    {
        question: "In what year was the Treaty of Versailles signed?",
        answers: ["1918", "1919", "1920", "1923"],
        correct: "1919"
    }
];

const cover = document.getElementById("cover");
const quiz = document.getElementById("quiz");
const gameCard = document.getElementById("game-card");
const result = document.getElementById("result");
const answersElement = document.getElementById("answers");
const feedback = document.getElementById("feedback");
const playfield = document.getElementById("playfield");
const star = document.getElementById("star");

let questionIndex = 0;
let score = 0;
let gameActive = false;
let starsCaught = 0;
let secondsLeft = 12;
let lastFrame = 0;
let gameStartedAt = 0;
let animationId = 0;
let timerId = 0;
let velocityX = 0;
let velocityY = 0;

function show(element) {
    element.classList.remove("hidden");
}

function hide(element) {
    element.classList.add("hidden");
}

function startQuiz() {
    questionIndex = 0;
    score = 0;
    hide(cover);
    hide(result);
    hide(gameCard);
    show(quiz);
    renderQuestion();
}

function renderQuestion() {
    const item = questions[questionIndex];
    document.getElementById("question-number").textContent =
        `Question ${questionIndex + 1} of ${questions.length}`;
    document.getElementById("score-display").textContent = `Score: ${score}`;
    document.getElementById("progress-bar").style.width =
        `${(questionIndex / questions.length) * 100}%`;
    document.getElementById("question").textContent = item.question;
    feedback.textContent = "";
    feedback.className = "";

    answersElement.replaceChildren();

    const shuffledAnswers = [...item.answers].sort(() => Math.random() - 0.5);
    shuffledAnswers.forEach(answer => {
        const button = document.createElement("button");
        button.type = "button";
        button.className = "answer";
        button.textContent = answer;
        button.addEventListener("click", () => submitAnswer(answer));
        answersElement.appendChild(button);
    });
}

function submitAnswer(answer) {
    const buttons = answersElement.querySelectorAll("button");
    buttons.forEach(button => button.disabled = true);

    if (answer === questions[questionIndex].correct) {
        score += 10;
        feedback.textContent = "Correct! On to the next question.";
        feedback.className = "good";

        window.setTimeout(() => {
            questionIndex++;
            if (questionIndex === questions.length) {
                finishQuiz();
            } else {
                renderQuestion();
            }
        }, 650);
        return;
    }

    feedback.textContent = "Not quite! Catch 3 stars to earn another try.";
    feedback.className = "bad";
    window.setTimeout(startCollectionGame, 500);
}

function finishQuiz() {
    hide(quiz);
    hide(gameCard);
    show(result);
    document.getElementById("final-score").textContent =
        `Your score: ${score} / ${questions.length * 10}`;
}

function startCollectionGame() {
    hide(quiz);
    show(gameCard);
    document.getElementById("game-message").textContent =
        "Click or tap the moving star!";
    hide(document.getElementById("retry-game"));

    starsCaught = 0;
    secondsLeft = 12;
    gameActive = true;
    lastFrame = 0;
    gameStartedAt = performance.now();
    document.getElementById("stars-count").textContent = "Stars: 0 / 3";
    document.getElementById("timer").textContent = "Time: 12";

    const bounds = playfield.getBoundingClientRect();
    star.style.left = `${Math.max(0, bounds.width / 2 - 27)}px`;
    star.style.top = `${Math.max(0, bounds.height / 2 - 27)}px`;
    setNewVelocity();

    cancelAnimationFrame(animationId);
    clearInterval(timerId);
    animationId = requestAnimationFrame(moveStar);
    timerId = window.setInterval(updateTimer, 100);
}

function setNewVelocity() {
    const angle = Math.random() * Math.PI * 2;
    const speed = 400 + Math.random() * 260;
    velocityX = Math.cos(angle) * speed;
    velocityY = Math.sin(angle) * speed;
}

function moveStar(timestamp) {
    if (!gameActive) return;

    const elapsed = lastFrame ? Math.min((timestamp - lastFrame) / 1000, 0.04) : 0;
    lastFrame = timestamp;

    const bounds = playfield.getBoundingClientRect();
    const maxX = Math.max(0, bounds.width - star.offsetWidth);
    const maxY = Math.max(0, bounds.height - star.offsetHeight);

    let x = parseFloat(star.style.left) || 0;
    let y = parseFloat(star.style.top) || 0;

    x += velocityX * elapsed;
    y += velocityY * elapsed;

    if (x <= 0 || x >= maxX) {
        velocityX *= -1;
        x = Math.max(0, Math.min(maxX, x));
    }
    if (y <= 0 || y >= maxY) {
        velocityY *= -1;
        y = Math.max(0, Math.min(maxY, y));
    }

    star.style.left = `${x}px`;
    star.style.top = `${y}px`;
    animationId = requestAnimationFrame(moveStar);
}

function updateTimer() {
    const elapsed = (performance.now() - gameStartedAt) / 1000;
    secondsLeft = Math.max(0, 12 - Math.floor(elapsed));
    document.getElementById("timer").textContent = `Time: ${secondsLeft}`;

    if (secondsLeft <= 0) {
        stopGame();
        document.getElementById("game-message").textContent =
            "Time’s up! Give it another try.";
        show(document.getElementById("retry-game"));
    }
}

function stopGame() {
    gameActive = false;
    cancelAnimationFrame(animationId);
    clearInterval(timerId);
}

function collectStar() {
    if (!gameActive) return;

    starsCaught++;
    document.getElementById("stars-count").textContent =
        `Stars: ${starsCaught} / 3`;

    if (starsCaught >= 3) {
        stopGame();
        document.getElementById("game-message").textContent =
            "Nice catching! You can retry the question.";
        star.disabled = true;

        window.setTimeout(() => {
            star.disabled = false;
            hide(gameCard);
            show(quiz);
            feedback.textContent = "Challenge complete — choose your answer again!";
            feedback.className = "good";
            answersElement.querySelectorAll("button").forEach(button => {
                button.disabled = false;
            });
        }, 700);
        return;
    }

    // Move the star to a new location immediately after each catch.
    const bounds = playfield.getBoundingClientRect();
    const maxX = Math.max(0, bounds.width - star.offsetWidth);
    const maxY = Math.max(0, bounds.height - star.offsetHeight);
    star.style.left = `${Math.random() * maxX}px`;
    star.style.top = `${Math.random() * maxY}px`;
    setNewVelocity();
}

document.getElementById("start-button").addEventListener("click", startQuiz);
document.getElementById("retry-game").addEventListener("click", startCollectionGame);
document.getElementById("play-again").addEventListener("click", startQuiz);
star.addEventListener("click", collectStar);

document.getElementById("funny-button").addEventListener("click", event => {
    const picture = document.getElementById("funny-picture");
    const isHidden = picture.classList.toggle("hidden");
    event.currentTarget.setAttribute("aria-expanded", String(!isHidden));
    event.currentTarget.textContent = isHidden
        ? "Show more"
        : "🙈 Hidepicture";
});
</script>
</body>
</html>
