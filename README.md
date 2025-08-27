[index.html](https://github.com/user-attachments/files/22001555/index.html)

<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Chúc mừng sinh nhật</title>
  <style>
    body, html {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      overflow: hidden;
      background: black;
      font-family: 'Courier New', monospace;
    }
    canvas {
      position: absolute;
      top: 0;
      left: 0;
      z-index: 0;
    }
    .wish {
      position: absolute;
      color: #00ff99;
      font-size: 30px;
      font-weight: bold;
      text-shadow: 0 0 10px #0f0, 0 0 20px #0f0;
      opacity: 0;
      transition: opacity 1s, transform 1s;
      z-index: 1;
    }
    .signature {
      position: absolute;
      top: 10px;
      right: 20px;
      font-size: 22px;
      font-weight: bold;
      background: linear-gradient(90deg, red, orange, yellow, lime, cyan, blue, violet);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      animation: rainbow 3s linear infinite;
    }
    @keyframes rainbow {
      0% { background-position: 0% 50%; }
      100% { background-position: 100% 50%; }
    }
  </style>
</head>
<body>
  <canvas id="matrix"></canvas>
  <div class="signature">Hải thành (minazure)</div>
  <script>
    // Nền hacker matrix
    const canvas = document.getElementById('matrix');
    const ctx = canvas.getContext('2d');
    canvas.height = window.innerHeight;
    canvas.width = window.innerWidth;

    const letters = '01';
    const fontSize = 16;
    const columns = canvas.width / fontSize;
    const drops = [];
    for (let x = 0; x < columns; x++) drops[x] = 1;

    function drawMatrix() {
      ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
      ctx.fillRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = '#0F0';
      ctx.font = fontSize + 'px monospace';
      for (let i = 0; i < drops.length; i++) {
        const text = letters.charAt(Math.floor(Math.random() * letters.length));
        ctx.fillText(text, i * fontSize, drops[i] * fontSize);
        if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
          drops[i] = 0;
        }
        drops[i]++;
      }
    }
    setInterval(drawMatrix, 33);

    // Lời chúc ngẫu nhiên
    const wishes = [
      "✨ Bích Hằng ✨",
      "Chúc mừng sinh nhật tuổi 16!",
      "Càng ngày càng xinh đẹp 💖",
      "Luôn vui vẻ và hạnh phúc 🎉",
      "Have a wonderful day! 🌟"
    ];

    function showWish() {
      const wish = document.createElement("div");
      wish.className = "wish";
      wish.innerText = wishes[Math.floor(Math.random() * wishes.length)];
      document.body.appendChild(wish);

      const x = Math.random() * (window.innerWidth - 200);
      const y = Math.random() * (window.innerHeight - 100);
      wish.style.left = x + "px";
      wish.style.top = y + "px";

      setTimeout(() => {
        wish.style.opacity = 1;
        wish.style.transform = "scale(1.2)";
      }, 100);

      setTimeout(() => {
        wish.style.opacity = 0;
        wish.style.transform = "scale(0.5)";
        setTimeout(() => { wish.remove(); }, 1000);
      }, 4000);
    }
    setInterval(showWish, 2000);
  </script>
</body>
</html>
