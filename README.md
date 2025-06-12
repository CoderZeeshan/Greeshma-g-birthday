<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Birthday Greeshma 🎂</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;700&display=swap');

    body {
      margin: 0;
      padding: 0;
      font-family: 'Pacifico', cursive;
      background: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
      overflow: hidden;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      color: #fff;
      text-align: center;
    }

    h1 {
      opacity: 0;
      transition: opacity 1s ease-in-out;
    }

    p {
      opacity: 0;
      transition: opacity 1s ease-in-out;
      font-family: 'Open Sans', sans-serif;
      font-size: 1.2em;
      font-weight: 400;
    }

    .show {
      opacity: 1;
    }

    .button {
      padding: 0.7em 1.5em;
      background: #fff;
      color: #ff69b4;
      border: none;
      border-radius: 30px;
      font-size: 1em;
      cursor: pointer;
      margin-top: 1em;
      transition: background 0.3s ease;
    }

    .button:hover {
      background: #ffe6f0;
    }

    canvas {
      position: absolute;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 0;
    }
  </style>
</head>
<body>
  <canvas id="confetti"></canvas>

  <h1 id="birthdayMsg">🎉 Happy Birthday Greeshma! 🎉</h1>
  <p id="wishPara">May your day be filled with laughter, and all the anime you adore! Keep shining like the star you are 💫</p>

  <button class="button" onclick="revealMsg('birthdayMsg')">Click for Surprise 🎁</button>
  <button class="button" onclick="revealMsg('wishPara')">Click for a Message 💌</button>

  <audio autoplay loop>
    <source src="https://cdn.pixabay.com/download/audio/2023/04/01/audio_46357c3e3a.mp3?filename=happy-birthday-to-you-14001.mp3" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <script>
    document.getElementById("birthdayMsg").classList.remove("show");
    document.getElementById("wishPara").classList.remove("show");

    function revealMsg(id) {
      document.getElementById(id).classList.add("show");
    }

    // Confetti animation
    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const confetti = Array.from({ length: 150 }, () => ({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      r: Math.random() * 6 + 2,
      d: Math.random() * 100,
      color: `hsl(${Math.random() * 360}, 100%, 70%)`,
      tilt: Math.random() * 10 - 10,
      tiltAngle: 0,
      tiltAngleIncrement: Math.random() * 0.1
    }));

    function drawConfetti() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      confetti.forEach(c => {
        ctx.beginPath();
        ctx.lineWidth = c.r;
        ctx.strokeStyle = c.color;
        ctx.moveTo(c.x + c.tilt + c.r / 2, c.y);
        ctx.lineTo(c.x + c.tilt, c.y + c.tilt + c.r / 2);
        ctx.stroke();
      });
      updateConfetti();
    }

    function updateConfetti() {
      confetti.forEach(c => {
        c.tiltAngle += c.tiltAngleIncrement;
        c.y += Math.cos(c.d) + 1 + c.r / 2;
        c.tilt = Math.sin(c.tiltAngle) * 15;

        if (c.y > canvas.height) {
          c.y = -10;
          c.x = Math.random() * canvas.width;
        }
      });
    }

    setInterval(drawConfetti, 20);
  </script>
</body>
</html>
