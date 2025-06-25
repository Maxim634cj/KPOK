<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Рулетка подарков</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #0088cc, #4a90e2);
      color: #fff;
      text-align: center;
      padding: 30px;
    }
    .container {
      background: rgba(0,0,0,0.3);
      border-radius: 12px;
      padding: 20px;
      max-width: 400px;
      margin: auto;
    }
    h1 {
      font-size: 2em;
    }
    .wheel-container {
      position: relative;
      width: 300px;
      height: 300px;
      margin: 30px auto;
    }
    .wheel {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      border: 8px solid #fff;
      overflow: hidden;
      position: relative;
      transition: transform 4s cubic-bezier(.17,.67,.83,.67);
    }
    .pointer {
      position: absolute;
      top: -30px;
      left: 50%;
      transform: translateX(-50%);
      width: 0;
      height: 0;
      border-left: 20px solid transparent;
      border-right: 20px solid transparent;
      border-bottom: 30px solid white;
      z-index: 2;
    }
    .sector {
      position: absolute;
      width: 50%;
      height: 50%;
      top: 0;
      left: 50%;
      transform-origin: 0% 100%;
      clip-path: polygon(0 100%, 100% 100%, 100% 0);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 14px;
      font-weight: bold;
      color: #fff;
      text-shadow: 1px 1px 2px #000;
    }
    .btn {
      margin-top: 20px;
      padding: 12px 24px;
      font-size: 1.1em;
      background: gold;
      color: #000;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    .btn:hover {
      background: #e0c000;
    }
    #stars {
      margin: 10px 0;
      font-size: 1.1em;
    }
    #result {
      font-size: 1.2em;
      margin-top: 20px;
    }
  </style>
</head>
<body>

<div class="container">
  <h1>🎁 Рулетка подарков</h1>
  <p>Крути колесо за ⭐ и получай Telegram-подарки!</p>
  <div id="stars">⭐ Звезды: <span id="starCount">3</span></div>

  <div class="wheel-container">
    <div class="pointer"></div>
    <div class="wheel" id="wheel">
      <div class="sector" style="background:#f44336; transform: rotate(0deg);">🎉 Стикеры</div>
      <div class="sector" style="background:#4caf50; transform: rotate(60deg);">💎 Premium</div>
      <div class="sector" style="background:#2196f3; transform: rotate(120deg);">🎬 Видео</div>
      <div class="sector" style="background:#ffeb3b; color: #000; transform: rotate(180deg);">🎨 Аватарка</div>
      <div class="sector" style="background:#00bcd4; transform: rotate(240deg);">🤖 Бот-доступ</div>
      <div class="sector" style="background:#9c27b0; transform: rotate(300deg);">📦 Сюрприз</div>
    </div>
  </div>

  <button class="btn" onclick="spinWheel()">Крутить!</button>
  <p id="result"></p>

  <a href="https://t.me/YourTelegramBot" class="btn">Запустить бота</a>
</div>

<script>
  let angle = 0;
  let stars = 3;
  const wheel = document.getElementById("wheel");
  const result = document.getElementById("result");
  const starCount = document.getElementById("starCount");

  function spinWheel() {
    if (stars <= 0) {
      result.innerText = "У тебя закончились звёзды 😢";
      return;
    }

    stars--;
    starCount.innerText = stars;

    const spin = Math.floor(Math.random() * 360) + 1440;
    angle += spin;
    wheel.style.transform = "rotate(" + angle + "deg)";

    setTimeout(() => {
      const section = Math.floor(((angle % 360) + 30) / 60) % 6;
      const prizes = ["🎉 Стикеры", "💎 Premium", "🎬 Видео", "🎨 Аватарка", "🤖 Бот-доступ", "📦 Сюрприз"];
      const prize = prizes[section];
      result.innerText = "Ты выиграл: " + prize;

      // Здесь можно отправить POST-запрос в Telegram-бота
      // fetch('https://yourserver.com/api/win', {
      //   method: 'POST',
      //   headers: { 'Content-Type': 'application/json' },
      //   body: JSON.
      stringify({ userId: 'USER_ID', prize: prize })
      // });
    }, 4200);
  }
</script>

</body>
</html>
