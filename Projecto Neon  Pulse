<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<title>Project Neon Pulse - Versão 1.0</title>

<style>
* {
    box-sizing: border-box;
    -webkit-tap-highlight-color: transparent;
    user-select: none;
}

html, body {
    margin: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    background: #000;
    font-family: Arial, Helvetica, sans-serif;
    color: white;
}

body {
    display: flex;
    justify-content: center;
    align-items: center;
    touch-action: manipulation;
}

#game {
    position: relative;
    width: 100vw;
    height: 100dvh;
    max-width: 600px;
    overflow: hidden;
    background:
        radial-gradient(circle at 50% 50%, #100018 0%, #000 55%),
        #000;
}

/* Efeito de brilho do fundo */
#game::before {
    content: "";
    position: absolute;
    inset: 0;
    pointer-events: none;
    background:
        radial-gradient(circle at 50% 50%, rgba(255,0,140,.08), transparent 35%);
}

/* HUD */
#hud {
    position: absolute;
    top: 20px;
    left: 0;
    width: 100%;
    z-index: 20;
    text-align: center;
    pointer-events: none;
}

#title {
    font-size: clamp(14px, 4vw, 22px);
    letter-spacing: 4px;
    color: #ff159d;
    text-shadow:
        0 0 5px #ff159d,
        0 0 15px #ff159d,
        0 0 30px #ff159d;
    font-weight: 900;
}

#score {
    margin-top: 8px;
    font-size: clamp(32px, 10vw, 58px);
    font-weight: 900;
    text-shadow:
        0 0 8px #fff,
        0 0 20px #00ff66;
}

#best {
    font-size: 13px;
    color: #aaa;
    letter-spacing: 2px;
}

/* Área principal */
#arena {
    position: absolute;
    top: 15%;
    bottom: 13%;
    left: 0;
    width: 100%;
}

/* Zona alvo */
#target {
    position: absolute;
    left: 50%;
    top: 50%;
    width: min(46vw, 210px);
    height: min(46vw, 210px);
    transform: translate(-50%, -50%);
    border: 5px solid #39ff14;
    border-radius: 50%;
    box-shadow:
        0 0 8px #39ff14,
        0 0 20px #39ff14,
        0 0 45px rgba(57,255,20,.8),
        inset 0 0 25px rgba(57,255,20,.5);
}

/* Centro perfeito */
#target::after {
    content: "";
    position: absolute;
    left: 50%;
    top: 50%;
    width: 18%;
    height: 18%;
    transform: translate(-50%, -50%);
    border-radius: 50%;
    background: #39ff14;
    box-shadow:
        0 0 10px #39ff14,
        0 0 25px #39ff14,
        0 0 50px #39ff14;
}

/* Linha scanner */
#scanner {
    position: absolute;
    left: 7%;
    width: 86%;
    height: 5px;
    border-radius: 10px;
    background: #ff159d;
    box-shadow:
        0 0 5px #ff159d,
        0 0 15px #ff159d,
        0 0 35px #ff159d,
        0 0 70px rgba(255,21,157,.8);
    transform: translateY(-50%);
    z-index: 5;
}

#scanner::before,
#scanner::after {
    content: "";
    position: absolute;
    top: 50%;
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background: #ff159d;
    box-shadow:
        0 0 10px #ff159d,
        0 0 25px #ff159d;
}

#scanner::before {
    left: -7px;
    transform: translateY(-50%);
}

#scanner::after {
    right: -7px;
    transform: translateY(-50%);
}

/* Linha central visual */
#centerLine {
    position: absolute;
    left: 50%;
    top: 7%;
    bottom: 7%;
    width: 1px;
    transform: translateX(-50%);
    background: rgba(255,255,255,.08);
}

/* Instrução */
#instruction {
    position: absolute;
    bottom: 5%;
    left: 0;
    width: 100%;
    text-align: center;
    color: #aaa;
    font-size: 14px;
    letter-spacing: 2px;
    animation: pulseText 1.4s infinite;
}

@keyframes pulseText {
    0%,100% { opacity: .5; }
    50% { opacity: 1; }
}

/* Partículas */
.particle {
    position: absolute;
    width: 7px;
    height: 7px;
    border-radius: 50%;
    background: #39ff14;
    box-shadow:
        0 0 8px #39ff14,
        0 0 20px #39ff14;
    pointer-events: none;
    z-index: 50;
    animation: particleFly .7s ease-out forwards;
}

@keyframes particleFly {
    from {
        transform: translate(0,0) scale(1);
        opacity: 1;
    }
    to {
        transform:
            translate(var(--dx), var(--dy))
            scale(0);
        opacity: 0;
    }
}

/* Flash */
#flash {
    position: fixed;
    inset: 0;
    background: white;
    opacity: 0;
    pointer-events: none;
    z-index: 100;
}

.flashActive {
    animation: flashAnimation .18s ease-out;
}

@keyframes flashAnimation {
    0% { opacity: .9; }
    100% { opacity: 0; }
}

/* Tela inicial/Game Over */
.overlay {
    position: absolute;
    inset: 0;
    z-index: 200;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 25px;
    background: rgba(0,0,0,.88);
    backdrop-filter: blur(8px);
}

.panel {
    width: min(90vw, 430px);
    padding: 30px 22px;
    border: 1px solid rgba(255,21,157,.6);
    border-radius: 22px;
    text-align: center;
    background: rgba(5,5,10,.95);
    box-shadow:
        0 0 20px rgba(255,21,157,.3),
        inset 0 0 25px rgba(255,21,157,.04);
}

.panel h1 {
    margin: 0 0 10px;
    color: #ff159d;
    font-size: clamp(25px, 8vw, 42px);
    text-shadow:
        0 0 10px #ff159d,
        0 0 30px #ff159d;
}

.panel p {
    color: #aaa;
    line-height: 1.5;
}

.finalScore {
    margin: 18px 0 4px;
    font-size: 52px;
    font-weight: 900;
    color: #39ff14;
    text-shadow:
        0 0 10px #39ff14,
        0 0 30px #39ff14;
}

.finalBest {
    color: #fff;
    margin-bottom: 20px;
}

/* Botões */
button {
    width: 100%;
    border: none;
    border-radius: 14px;
    padding: 17px 12px;
    margin-top: 12px;
    font-size: 16px;
    font-weight: 900;
    letter-spacing: 1px;
    color: #000;
    background: #39ff14;
    box-shadow:
        0 0 10px #39ff14,
        0 0 25px rgba(57,255,20,.5);
    cursor: pointer;
}

button:active {
    transform: scale(.96);
}

.share {
    background: #ff159d;
    box-shadow:
        0 0 10px #ff159d,
        0 0 25px rgba(255,21,157,.5);
}

.hidden {
    display: none !important;
}

/* Texto de nível */
#levelText {
    position: absolute;
    left: 0;
    width: 100%;
    top: 44%;
    text-align: center;
    font-size: 16px;
    color: #fff;
    opacity: 0;
    pointer-events: none;
    text-shadow: 0 0 10px white;
    z-index: 30;
}

.levelPop {
    animation: levelAnimation .6s ease-out;
}

@keyframes levelAnimation {
    0% {
        opacity: 0;
        transform: scale(.5);
    }
    40% {
        opacity: 1;
        transform: scale(1.3);
    }
    100% {
        opacity: 0;
        transform: scale(1);
    }
}

/* Celulares muito pequenos */
@media (max-height: 600px) {
    #arena {
        top: 17%;
        bottom: 10%;
    }

    #target {
        width: 150px;
        height: 150px;
    }

    #instruction {
        bottom: 2%;
    }
}
</style>
</head>

<body>

<div id="game">

    <div id="hud">
        <div id="title">PROJECT NEON PULSE</div>
        <div id="score">0</div>
        <div id="best">RECORDE: 0</div>
    </div>

    <div id="arena">

        <div id="centerLine"></div>

        <div id="target"></div>

        <div id="scanner"></div>

        <div id="levelText"></div>

    </div>

    <div id="instruction">
        TOQUE NO MOMENTO CERTO
    </div>

    <div id="flash"></div>

    <!-- Tela inicial -->
    <div id="startScreen" class="overlay">
        <div class="panel">
            <h1>NEON<br>PULSE</h1>

            <p>
                Pare a linha dentro do alvo.<br>
                Acerte o centro perfeito para ganhar pontos.
            </p>

            <button id="startButton">
                ▶ COMEÇAR
            </button>
        </div>
    </div>

    <!-- Game Over -->
    <div id="gameOverScreen" class="overlay hidden">
        <div class="panel">

            <h1>GAME OVER</h1>

            <p>Seu resultado:</p>

            <div id="finalScore" class="finalScore">
                0
            </div>

            <div id="finalBest" class="finalBest">
                Recorde: 0
            </div>

            <button id="restartButton">
                🔄 JOGAR NOVAMENTE
            </button>

            <button id="shareButton" class="share">
                📋 COPIAR RESULTADO<br>
                PARA DESAFIAR AMIGOS
            </button>

            <p id="copyStatus"></p>

        </div>
    </div>

</div>

<script>
/* =========================================================
   PROJECT NEON PULSE
   VERSÃO 1.0
   ========================================================= */

const game = document.getElementById("game");
const arena = document.getElementById("arena");
const scanner = document.getElementById("scanner");
const target = document.getElementById("target");

const scoreElement = document.getElementById("score");
const bestElement = document.getElementById("best");

const startScreen = document.getElementById("startScreen");
const gameOverScreen = document.getElementById("gameOverScreen");

const startButton = document.getElementById("startButton");
const restartButton = document.getElementById("restartButton");
const shareButton = document.getElementById("shareButton");

const finalScore = document.getElementById("finalScore");
const finalBest = document.getElementById("finalBest");

const flash = document.getElementById("flash");
const levelText = document.getElementById("levelText");
const copyStatus = document.getElementById("copyStatus");

/* =========================
   CONFIGURAÇÕES
========================= */

const CONFIG = {
    pointsPerHit: 10,

    // Tolerância para acertar o alvo
    targetTolerance: 1,

    // Quanto menor, mais difícil
    perfectTolerance: 0.22,

    // Velocidade inicial
    initialSpeed: 0.004,

    // Aumento de velocidade por nível
    speedIncrease: 0.0007,

    // Limite máximo
    maxSpeed: 0.025
};

/* =========================
   ESTADO DO JOGO
========================= */

let score = 0;
let bestScore = Number(localStorage.getItem("neonPulseHighScore")) || 0;

let level = 1;

let running = false;
let direction = 1;

let position = 0.5;

let speed = CONFIG.initialSpeed;

let animationFrame = null;

bestElement.textContent = "RECORDE: " + bestScore;

/* =========================
   INICIAR
========================= */

function startGame() {

    score = 0;
    level = 1;
    speed = CONFIG.initialSpeed;

    position = 0.05;
    direction = 1;

    running = true;

    scoreElement.textContent = score;

    startScreen.classList.add("hidden");
    gameOverScreen.classList.add("hidden");

    copyStatus.textContent = "";

    cancelAnimationFrame(animationFrame);

    gameLoop();
}

/* =========================
   LOOP PRINCIPAL
========================= */

function gameLoop() {

    if (!running) return;

    position += direction * speed;

    if (position >= 0.95) {
        position = 0.95;
        direction = -1;
    }

    if (position <= 0.05) {
        position = 0.05;
        direction = 1;
    }

    const arenaHeight = arena.clientHeight;

    scanner.style.top = (position * 100) + "%";

    animationFrame = requestAnimationFrame(gameLoop);
}

/* =========================
   TOQUE DO JOGADOR
========================= */

function handleTap(event) {

    if (!running) return;

    event.preventDefault();

    checkHit();
}

/* =========================
   VERIFICAR ACERTO
========================= */

function checkHit() {

    const scannerRect = scanner.getBoundingClientRect();
    const targetRect = target.getBoundingClientRect();

    const scannerY =
        scannerRect.top + scannerRect.height / 2;

    const targetCenter =
        targetRect.top + targetRect.height / 2;

    const targetRadius =
        targetRect.height / 2;

    const distance =
        Math.abs(scannerY - targetCenter);

    /*
       Se a linha estiver completamente
       fora do círculo, Game Over.
    */

    if (distance > targetRadius) {
        gameOver();
        return;
    }

    /*
       Calcula o quão próximo
       o jogador chegou do centro.
    */

    const accuracy =
        distance / targetRadius;

    if (accuracy <= CONFIG.perfectTolerance) {

        perfectHit();

    } else {

        normalHit();
    }
}

/* =========================
   ACERTO PERFEITO
========================= */

function perfectHit() {

    score += CONFIG.pointsPerHit;

    scoreElement.textContent = score;

    level++;

    speed = Math.min(
        CONFIG.maxSpeed,
        CONFIG.initialSpeed +
        (level - 1) * CONFIG.speedIncrease
    );

    createParticles();

    flash.classList.remove("flashActive");

    /*
       Força o navegador a reiniciar
       a animação do flash.
    */
    void flash.offsetWidth;

    flash.classList.add("flashActive");

    showLevelText();

    /*
       Pequena vibração em celulares
       que suportam a API.
    */
    if (navigator.vibrate) {
        navigator.vibrate([20, 30, 20]);
    }
}

/* =========================
   ACERTO NORMAL
========================= */

function normalHit() {

    score += 5;

    scoreElement.textContent = score;

    if (navigator.vibrate) {
        navigator.vibrate(15);
    }
}

/* =========================
   TEXTO DE NÍVEL
========================= */

function showLevelText() {

    levelText.textContent =
        "PERFEITO!  +10  •  NÍVEL " + level;

    levelText.classList.remove("levelPop");

    void levelText.offsetWidth;

    levelText.classList.add("levelPop");
}

/* =========================
   PARTÍCULAS
========================= */

function createParticles() {

    const rect = target.getBoundingClientRect();

    const gameRect = game.getBoundingClientRect();

    const centerX =
        rect.left - gameRect.left + rect.width / 2;

    const centerY =
        rect.top - gameRect.top + rect.height / 2;

    for (let i = 0; i < 30; i++) {

        const particle =
            document.createElement("div");

        particle.className = "particle";

        particle.style.left =
            centerX + "px";

        particle.style.top =
            centerY + "px";

        const angle =
            Math.random() * Math.PI * 2;

        const distance =
            50 + Math.random() * 150;

        const dx =
            Math.cos(angle) * distance;

        const dy =
            Math.sin(angle) * distance;

        particle.style.setProperty(
            "--dx",
            dx + "px"
        );

        particle.style.setProperty(
            "--dy",
            dy + "px"
        );

        const size =
            3 + Math.random() * 7;

        particle.style.width =
            size + "px";

        particle.style.height =
            size + "px";

        game.appendChild(particle);

        setTimeout(() => {
            particle.remove();
        }, 700);
    }
}

/* =========================
   GAME OVER
========================= */

function gameOver() {

    running = false;

    cancelAnimationFrame(animationFrame);

    if (navigator.vibrate) {
        navigator.vibrate([100, 80, 100]);
    }

    /*
       Atualiza recorde.
    */

    if (score > bestScore) {

        bestScore = score;

        localStorage.setItem(
            "neonPulseHighScore",
            bestScore
        );
    }

    bestElement.textContent =
        "RECORDE: " + bestScore;

    finalScore.textContent =
        score;

    finalBest.textContent =
        "Recorde: " + bestScore;

    gameOverScreen.classList.remove("hidden");
}

/* =========================
   COPIAR RESULTADO
========================= */

async function shareResult() {

    /*
       Troque pelo endereço real
       quando publicar o jogo.
    */

    const gameLink =
        window.location.href;

    const message =
`🔥 Bati o recorde na Versão 1.0!
🎯 Pontuação: ${score}
⚡ Recorde Máximo: ${bestScore}
Quero ver você passar disso! Jogue aqui: ${gameLink}`;

    try {

        await navigator.clipboard.writeText(message);

        copyStatus.textContent =
            "✅ Resultado copiado!";

        if (navigator.vibrate) {
            navigator.vibrate(30);
        }

    } catch (error) {

        /*
           Fallback para navegadores
           que não permitem clipboard.
        */

        const textArea =
            document.createElement("textarea");

        textArea.value = message;

        document.body.appendChild(textArea);

        textArea.select();

        try {
            document.execCommand("copy");

            copyStatus.textContent =
                "✅ Resultado copiado!";
        } catch (e) {

            copyStatus.textContent =
                "❌ Não foi possível copiar automaticamente.";
        }

        textArea.remove();
    }
}

/* =========================
   EVENTOS
========================= */

startButton.addEventListener(
    "click",
    startGame
);

restartButton.addEventListener(
    "click",
    startGame
);

shareButton.addEventListener(
    "click",
    shareResult
);

/*
   Touch.
*/

game.addEventListener(
    "touchstart",
    handleTap,
    { passive: false }
);

/*
   Clique também funciona
   para testar no navegador.
*/

game.addEventListener(
    "mousedown",
    handleTap
);

/*
   Impede zoom por gesto.
*/

document.addEventListener(
    "gesturestart",
    function(event) {
        event.preventDefault();
    }
);

/*
   Impede menu de contexto.
*/

document.addEventListener(
    "contextmenu",
    function(event) {
        event.preventDefault();
    }
);

/* =========================
   GARANTE POSIÇÃO INICIAL
========================= */

scanner.style.top = "5%";
</script>

</body>
</html>
