<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Валентинка с летающими сердцами</title>
  <style>
    body, html {
      margin: 0;
      height: 100vh;
      overflow: hidden;
      background: #000;
      font-family: 'Montserrat', sans-serif;
      position: relative;
    }

    .container {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: rgba(255 255 255 / 0.95);
      border-radius: 20px;
      padding: 30px 30px 40px 30px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.2);
      min-width: 320px;
      max-width: 380px;
      text-align: center;
      color: #332f6f;
      user-select: none;
      z-index: 10;
      overflow: hidden;
    }

    .container h1 {
      font-weight: 700;
      font-size: 28px;
      margin-bottom: 8px;
    }

    .container p {
      font-weight: 400;
      font-size: 17px;
      margin-bottom: 25px;
      color: #000;
    }

    button {
      cursor: pointer;
      font-weight: 700;
      font-size: 16px;
      border-radius: 9999px;
      border: none;
      padding: 12px 26px;
      margin: 0 10px;
      transition: all 0.3s ease;
      user-select: none;
      position: relative;
      z-index: 10;
    }

    #yesBtn {
      background: #5459db;
      color: #fff;
      box-shadow: 0 8px 10px rgb(84 89 219 / 0.5);
    }

    #yesBtn:hover {
      filter: brightness(1.1);
    }

    #noBtn {
      background: #ccc;
      color: #555;
      position: absolute;
      top: 50%;
      left: calc(50% + 90px);
      transform: translate(-50%, -50%);
      transition: none;
      z-index: 10;
      user-select: none;
    }

    .result {
      color: #332f6f;
    }

    .result h2 {
      font-size: 24px;
      margin-bottom: 20px;
      user-select: text;
    }

    .result img {
      max-width: 140px;
      margin: 10px 12px;
      border-radius: 12px;
      box-shadow: 0 6px 15px rgba(255, 0, 90, 0.3);
      vertical-align: middle;
    }
    @keyframes floatUp {
      0% {
        transform: translateY(100vh) scale(1);
        opacity: 1;
      }
      100% {
        transform: translateY(-50px) scale(0.5);
        opacity: 0;
      }
    }
  </style>
</head>
<body>
  <div class="container" id="popup">
    <h1>💝 Для Самой Лучшей 💝</h1>
    <p>Будешь моей Валентинкой?</p>
    <button id="yesBtn">Да! 💞</button>
    <button id="noBtn">Нет</button>
  </div>

  <script>
    const noBtn = document.getElementById('noBtn');
    const yesBtn = document.getElementById('yesBtn');
    const popup = document.getElementById('popup');

    noBtn.addEventListener('mouseenter', () => {
      const containerRect = popup.getBoundingClientRect();
      const noBtnRect = noBtn.getBoundingClientRect();

      const maxX = containerRect.width - noBtnRect.width - 10;
      const maxY = containerRect.height - noBtnRect.height - 10;

      let newX = Math.floor(Math.random() * maxX);
      let newY = Math.floor(Math.random() * maxY);

      const yesBtnRect = yesBtn.getBoundingClientRect();
      const relativeYesX = yesBtnRect.left - containerRect.left;
      const relativeYesY = yesBtnRect.top - containerRect.top;

      if (Math.abs(newX - relativeYesX) < 50) {
        newX = (newX + 60) % maxX;
      }

      noBtn.style.left = newX + 'px';
      noBtn.style.top = newY + 'px';
    });

    yesBtn.addEventListener('click', () => {
      popup.innerHTML = `
        <div class="result">
          <h2>Спасибо! Ты самая лучшая! 💖</h2>
          <img src="https://i.gifer.com/origin/9d/9dfa6c5a686bbd7554f7a7a985ad5da4.gif" alt="Сердца" />
        </div>
      `;
      // Дополнительно можно добавить анимацию летающих сердечек (опционально)
      for (let i = 0; i < 20; i++) {
        const heart = document.createElement('div');
        heart.style.position = 'fixed';
        heart.style.left = Math.random() * 100 + 'vw';
        heart.style.top = '100vh';
        heart.style.width = '20px';
        heart.style.height = '20px';
        heart.style.background = 'red';
        heart.style.clipPath = 'polygon(50% 0%, 61% 18%, 98% 35%, 80% 63%, 50% 100%, 20% 63%, 2% 35%, 39% 18%)';
        heart.style.opacity = '0.7';
        heart.style.animation = `floatUp ${4 + Math.random() * 2}s linear forwards`;
        heart.style.animationDelay = (i * 0.2) + 's';
        document.body.appendChild(heart);
        setTimeout(() => heart.remove(), 6000);
      }
    });
  </script>
</body>
</html>
