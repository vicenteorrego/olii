<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Ajedrez - 2 Jugadores</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/chess.js/0.10.3/chess.min.js"></script>

<style>

/* =====================================================
   GENERAL
===================================================== */

* {
    box-sizing: border-box;
}

html,
body {
    margin: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;

    font-family: Arial, sans-serif;
}


/* =====================================================
   PANTALLA DE INICIO
===================================================== */

#home {
    width: 100%;
    height: 100vh;

    display: flex;
    justify-content: center;
    align-items: center;

    position: relative;
    overflow: hidden;

    background:
        radial-gradient(
            circle at 15% 20%,
            #ff6b6b,
            transparent 25%
        ),
        radial-gradient(
            circle at 85% 20%,
            #4dabf7,
            transparent 25%
        ),
        radial-gradient(
            circle at 50% 100%,
            #845ef7,
            transparent 35%
        ),
        linear-gradient(
            135deg,
            #667eea,
            #764ba2
        );
}

.home-card {
    width: min(90%, 560px);

    padding: 45px 30px;

    text-align: center;

    border-radius: 28px;

    background: rgba(255,255,255,.95);

    box-shadow:
        0 20px 60px rgba(0,0,0,.3);

    position: relative;

    z-index: 2;
}

.logo {
    font-size: 80px;
    margin-bottom: 5px;
}

.title {
    margin: 0;

    font-size: 58px;

    font-weight: bold;

    background:
        linear-gradient(
            90deg,
            #4285f4,
            #9c27b0,
            #ea4335,
            #fbbc05
        );

    -webkit-background-clip: text;

    color: transparent;
}

.subtitle {
    color: #5f6368;

    font-size: 19px;

    margin: 12px 0 30px;
}

.start-button {
    border: none;

    border-radius: 30px;

    padding: 15px 45px;

    font-size: 18px;

    font-weight: bold;

    color: white;

    cursor: pointer;

    background:
        linear-gradient(
            90deg,
            #4285f4,
            #8e44ad
        );

    box-shadow:
        0 7px 20px rgba(0,0,0,.2);

    transition: .2s;
}

.start-button:hover {
    transform:
        translateY(-3px)
        scale(1.04);
}


/* =====================================================
   PIEZAS DECORATIVAS
===================================================== */

.floating {
    position: absolute;

    color: white;

    opacity: .15;

    font-size: 100px;

    animation:
        float 5s infinite ease-in-out;
}

.f1 {
    left: 8%;
    top: 15%;
}

.f2 {
    right: 8%;
    top: 18%;

    animation-delay: 1s;
}

.f3 {
    left: 12%;
    bottom: 10%;

    animation-delay: 2s;
}

.f4 {
    right: 12%;
    bottom: 12%;

    animation-delay: 3s;
}

@keyframes float {

    0%,100% {
        transform:
            translateY(0)
            rotate(-5deg);
    }

    50% {
        transform:
            translateY(-20px)
            rotate(5deg);
    }
}


/* =====================================================
   JUEGO
===================================================== */

#game {
    display: none;

    width: 100%;
    height: 100vh;

    overflow: hidden;

    padding: 8px 15px;

    background:
        radial-gradient(
            circle at 50% 0%,
            rgba(255,220,160,.2),
            transparent 30%
        ),
        linear-gradient(
            180deg,
            #33485c,
            #172333 60%,
            #101722
        );

    color: white;
}

.game-container {
    width: 100%;
    height: 100%;

    max-width: 1050px;

    margin: auto;

    display: flex;

    flex-direction: column;
}


/* =====================================================
   CABECERA
===================================================== */

.game-header {
    height: 45px;

    flex-shrink: 0;

    display: flex;

    justify-content: space-between;

    align-items: center;
}

.game-title {
    margin: 0;

    font-size: 27px;

    text-shadow:
        0 2px 5px black;
}

.back-button {
    border:
        1px solid
        rgba(255,255,255,.3);

    background:
        rgba(255,255,255,.12);

    color: white;

    padding:
        7px 13px;

    border-radius: 7px;

    cursor: pointer;
}

.back-button:hover {
    background:
        rgba(255,255,255,.25);
}


/* =====================================================
   ZONA PRINCIPAL
===================================================== */

.game-area {
    flex: 1;

    min-height: 0;

    display: flex;

    justify-content: center;

    align-items: center;

    gap: 25px;
}


/* =====================================================
   MARCADOR
===================================================== */

.scoreboard {
    width: 140px;

    flex-shrink: 0;

    display: flex;

    flex-direction: column;

    gap: 12px;
}

.score-card {
    background: white;

    color: #202124;

    border-radius: 14px;

    padding:
        14px 10px;

    text-align: center;

    box-shadow:
        0 7px 18px
        rgba(0,0,0,.35);
}

.score-name {
    font-size: 14px;

    color: #5f6368;

    margin-bottom: 5px;
}

.score {
    font-size: 32px;

    font-weight: bold;
}

.rounds {
    text-align: center;

    font-size: 13px;

    color: #e5e7eb;
}


/* =====================================================
   TABLERO
===================================================== */

.board-section {
    position: relative;

    display: flex;

    flex-direction: column;

    align-items: center;

    justify-content: center;
}


/* =====================================================
   BOTÓN NUEVA PARTIDA
===================================================== */

.controls {
    position: absolute;

    left: calc(100% + 22px);

    top: 50%;

   
