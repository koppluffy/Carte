<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Carte à Gratter - Bébé arrive</title>
  <style>
    body {
      font-family: "Comic Sans MS", cursive, sans-serif;
      background: #ffe7f0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    .scratch-card {
      position: relative;
      width: 320px;
      height: 320px;
      border-radius: 25px;
      overflow: hidden;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
      background-image: url('https://www.transparenttextures.com/patterns/confetti.png');
      background-color: #ffe7f0;
      background-size: cover;
    }

    #background {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 28px;
      font-weight: bold;
      text-align: center;
      color: #e63946;
      z-index: 0;
      padding: 20px;
    }

    canvas {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 1;
      touch-action: none;
      border-radius: 25px;
    }

    h2 {
      margin-bottom: 20px;
      text-align: center;
      color: #e63946;
    }
  </style>
</head>
<body>
  <h2>Gratte ici pour découvrir la surprise 🎁</h2>

  <div class="scratch-card">
    <div id="background">🎉 Surprise !<br>👶 Bébé arrive ❤️</div>
    <canvas id="scratchCanvas" width="320" height="320"></canvas>
  </div>

  <script>
    const canvas = document.getElementById("scratchCanvas");
    const ctx = canvas.getContext("2d");

    // Couche à gratter
    ctx.fillStyle = "#a8a8a8";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    let isDrawing = false;

    function getPointerPos(e) {
      const rect = canvas.getBoundingClientRect();
      const x = (e.touches ? e.touches[0].clientX : e.clientX) - rect.left;
      const y = (e.touches ? e.touches[0].clientY : e.clientY) - rect.top;
      return { x, y };
    }

    function startDrawing(e) {
      isDrawing = true;
      scratch(e);
    }

    function endDrawing() {
      isDrawing = false;
    }

    function scratch(e) {
      if (!isDrawing) return;
      const pos = getPointerPos(e);
      ctx.globalCompositeOperation = "destination-out";
      ctx.beginPath();
      ctx.arc(pos.x, pos.y, 20, 0, 2 * Math.PI);
      ctx.fill();
    }

    canvas.addEventListener("mousedown", startDrawing);
    canvas.addEventListener("mousemove", scratch);
    canvas.addEventListener("mouseup", endDrawing);
    canvas.addEventListener("touchstart", startDrawing);
    canvas.addEventListener("touchmove", scratch);
    canvas.addEventListener("touchend", endDrawing);
  </script>
</body>
</html>
