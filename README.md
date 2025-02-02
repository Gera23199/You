<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Carta de San Valentín</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background: radial-gradient(circle at bottom, #0d1b2a, #1b263b, #415a77);
            overflow: hidden;
            position: relative;
            color: white;
        }
        .stars {
            position: absolute;
            width: 100%;
            height: 100%;
            background: url('https://www.transparenttextures.com/patterns/stardust.png') repeat;
            z-index: 0;
        }
        .envelope {
            width: 300px;
            height: 200px;
            position: relative;
            background: #d32f2f;
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            overflow: hidden;
            z-index: 1;
        }
        .flap {
            position: absolute;
            top: 0;
            width: 100%;
            height: 100px;
            background: #b71c1c;
            clip-path: polygon(50% 0%, 100% 100%, 0% 100%);
            transform-origin: top;
            transition: transform 0.5s;
            z-index: 2;
        }
        .letter {
            position: absolute;
            width: 260px;
            height: 160px;
            background: white;
            top: 100%;
            text-align: center;
            padding: 20px;
            font-family: Arial, sans-serif;
            font-size: 18px;
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
            z-index: 1;
            display: none;
        }
        .buttons {
            margin-top: 15px;
        }
        button {
            padding: 10px;
            font-size: 16px;
            margin: 5px;
            border: none;
            cursor: pointer;
        }
        .yes {
            background: green;
            color: white;
        }
        .no {
            background: red;
            color: white;
        }
        .heart {
            position: absolute;
            width: 50px;
            height: 50px;
            background: red;
            transform: rotate(-45deg);
            top: 50%;
            left: 50%;
            margin: -25px;
        }
        .heart:before, .heart:after {
            content: "";
            position: absolute;
            width: 50px;
            height: 50px;
            background: red;
            border-radius: 50%;
        }
        .heart:before {
            top: -25px;
            left: 0;
        }
        .heart:after {
            left: 25px;
            top: 0;
        }
        .heart-float {
            position: absolute;
            bottom: -50px;
            animation: float 5s infinite ease-in;
        }
        .tulip {
            position: absolute;
            bottom: 0;
        }
        .message {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: rgba(0, 0, 0, 0.8);
            padding: 20px;
            border-radius: 10px;
            font-size: 20px;
            text-align: center;
            display: none;
            z-index: 10;
        }
        .message-text {
            font-size: 18px;
            margin-bottom: 20px;
        }
        .question {
            font-size: 24px;
            color: #ff69b4;
            font-weight: bold;
            text-align: center;
            display: none;
        }
        @keyframes float {
            0% { transform: translateY(0); opacity: 1; }
            100% { transform: translateY(-500px); opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="stars"></div>
    <div class="envelope" onclick="openEnvelope()">
        <div class="flap"></div>
        <div class="letter" id="letterBox">
            <div class="question" id="questionBox">💖 ¿Quieres ser mi San Valentín? 💖</div>
            <div class="buttons">
                <button class="yes" onclick="showMessage('¡Sí! Estoy muy feliz 💕')">Sí</button>
                <button class="no" onclick="showMessage('Oh... 😢')">No</button>
            </div>
        </div>
    </div>
    <div class="message" id="messageBox"></div>

    <script>
        function openEnvelope() {
            const flap = document.querySelector('.flap');
            const letter = document.querySelector('.letter');
            const questionBox = document.getElementById('questionBox');
            // Mostrar la carta al abrir el sobre
            gsap.to(flap, { rotateX: 180, duration: 0.5 });
            gsap.to(letter, { y: -200, duration: 0.5, delay: 0.5 });
            letter.style.display = 'block'; // Asegurarse de que la carta sea visible

            // Mostrar la pregunta "¿Quieres ser mi San Valentín?"
            questionBox.style.display = 'block';
        }

        function showMessage(message) {
            const messageBox = document.getElementById('messageBox');
            messageBox.textContent = message;
            messageBox.style.display = 'block';
        }

        function createHeart() {
            const heart = document.createElement("div");
            heart.classList.add("heart", "heart-float");
            heart.style.left = Math.random() * 100 + "vw";
            heart.style.animationDuration = Math.random() * 2 + 3 + "s";
            document.body.appendChild(heart);
            setTimeout(() => heart.remove(), 5000);
        }
        setInterval(createHeart, 500);

        function createTulip(x, y, color) {
            const tulip = document.createElementNS("http://www.w3.org/2000/svg", "svg");
            tulip.setAttribute("width", "50");
            tulip.setAttribute("height", "100");
            tulip.setAttribute("viewBox", "0 0 50 100");
            tulip.setAttribute("class", "tulip");
            tulip.style.left = `${x}px`;
            tulip.style.bottom = `${y}px`;
            tulip.innerHTML = `
                <path d="M25 0 C30 20, 50 20, 25 50 C0 20, 20 20, 25 0" fill="${color}" />
                <rect x="23" y="50" width="4" height="50" fill="green" />
                <path d="M23 70 C15 60, 5 60, 15 75" fill="green" />
                <path d="M27 70 C35 60, 45 60, 35 75" fill="green" />
            `;
            document.body.appendChild(tulip);
        }

        for (let i = 0; i < 20; i++) {
            const color = i % 2 === 0 ? "purple" : "blue";
            createTulip(i * 80 + 50, 0, color);
        }
    </script>
</body>
</html>
