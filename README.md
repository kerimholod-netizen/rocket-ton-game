<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>🚀 Rocket Stars</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <script type="module" src="https://unpkg.com/@tonconnect/ui@latest"></script>
  <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet">
  <style>
    body {
      margin: 0;
      font-family: 'Press Start 2P', cursive;
      background: url('https://i.ibb.co/hFZpMhp/stars-bg.gif') repeat;
      background-size: cover;
      color: #00ffe1;
      text-align: center;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }

    h1 {
      font-size: 24px;
      margin-bottom: 10px;
      color: #fff;
      text-shadow: 0 0 10px #0ff;
    }

    p {
      font-size: 12px;
      margin-bottom: 30px;
      color: #ccc;
    }

    .btn {
      background: transparent;
      border: 2px solid #00ffe1;
      padding: 16px 30px;
      margin: 12px;
      border-radius: 12px;
      font-size: 12px;
      color: #00ffe1;
      cursor: pointer;
      transition: 0.3s;
      text-transform: uppercase;
      box-shadow: 0 0 8px #00ffe1;
    }

    .btn:hover {
      background: #00ffe133;
      box-shadow: 0 0 15px #00ffe1, 0 0 40px #00ffe1;
    }

    #connect-button {
      margin-top: 30px;
    }

    .message {
      margin-top: 25px;
      font-size: 10px;
      color: #fff;
      text-shadow: 0 0 5px #00ffe1;
    }

    .rocket {
      width: 80px;
      height: 80px;
      margin: 20px auto;
      background: url('https://i.ibb.co/N6kpS20/pixel-rocket.gif') no-repeat center center;
      background-size: contain;
      animation: float 2s ease-in-out infinite;
    }

    @keyframes float {
      0% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
      100% { transform: translateY(0); }
    }
  </style>
</head>
<body>

  <div>
    <h1>🚀 ROCKET STARS</h1>
    <div class="rocket"></div>
    <p>Топливо куплено? Готовься к полёту!</p>

    <button class="btn" onclick="play()">🔥 Играть</button>
    <button class="btn" onclick="deposit()">💰 Пополнить</button>
    <button class="btn" onclick="withdraw()">📤 Вывести</button>
    <button class="btn" onclick="openProfile()">👤 Профиль</button>

    <div id="connect-button"></div>
    <div class="message" id="message"></div>
  </div>

  <script type="module">
    import { TonConnectUI } from "https://unpkg.com/@tonconnect/ui@latest";

    const tonConnectUI = new TonConnectUI({
      manifestUrl: "https://yourdomain.com/tonconnect-manifest.json", // замени на свой
      buttonRootId: "connect-button"
    });

    const messageEl = document.getElementById("message");

    window.play = () => {
      messageEl.textContent = "🚀 Ракета полетела в гиперпространство!";
    };

    window.deposit = async () => {
      messageEl.textContent = "💸 Отправка 0.01 TON в процессе...";
      try {
        await tonConnectUI.sendTransaction({
          validUntil: Math.floor(Date.now() / 1000) + 600,
          messages: [
            {
              address: "UQAqwXhqugjcRUWDqsxhmaZrm5XDoexVQD7RGCQED4DOCH2f", // твой TON
              amount: "10000000" // 0.01 TON
            }
          ]
        });
        messageEl.textContent = "✅ Успешно отправлено!";
      } catch (e) {
        messageEl.textContent = "❌ Отмена или ошибка при отправке TON.";
      }
    };

    window.withdraw = () => {
      messageEl.textContent = "📤 Обработка вывода средств...";
    };

    window.openProfile = () => {
      messageEl.textContent = "👤 Профиль открыт!";
    };
  </script>

</body>
</html>
