<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>Bugün Sahne Senin</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Georgia, serif;
    }

    body {
      width: 100%;
      height: 100vh;
      background: radial-gradient(circle at top, #111, #000);
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
    }

    /* BAŞLAT BUTONU */
    .start-screen {
      position: fixed;
      inset: 0;
      background: radial-gradient(circle at top, #111, #000);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      z-index: 50;
      gap: 20px;
    }

    .start-btn {
      padding: 22px 60px;
      font-size: 22px;
      border-radius: 60px;
      border: none;
      cursor: pointer;
      font-weight: bold;
      color: black;
      background: linear-gradient(135deg, gold, orange);
      box-shadow: 0 0 30px rgba(255,165,0,1);
    }

    /* PERDELER */
    .curtain {
      position: fixed;
      top: 0;
      width: 50%;
      height: 100%;
      background: linear-gradient(135deg, #7a0000, #b30000);
      z-index: 10;
      transition: transform 2.5s ease-in-out;
    }

    .curtain.left { left: 0; }
    .curtain.right { right: 0; }

    .curtain.open.left { transform: translateX(-100%); }
    .curtain.open.right { transform: translateX(100%); }

    /* SPOT */
    .spotlight {
      position: absolute;
      top: -20%;
      left: 50%;
      width: 320px;
      height: 900px;
      transform: translateX(-50%);
      background: radial-gradient(circle at top, rgba(255,255,255,0.45), transparent 70%);
      filter: blur(12px);
      animation: lightMove 6s infinite alternate;
      z-index: 0;
    }

    @keyframes lightMove {
      from { transform: translateX(-60%); }
      to { transform: translateX(-40%); }
    }

    /* SAHNE */
    .stage {
      text-align: center;
      opacity: 0;
      transform: scale(0.85);
      transition: 2s ease;
      z-index: 1;
      padding: 20px;
    }

    .stage.show {
      opacity: 1;
      transform: scale(1);
    }

    h1 {
      font-size: 46px;
      color: gold;
      text-shadow: 0 0 25px rgba(255,215,0,0.8);
      margin-bottom: 20px;
    }

    h2 {
      font-size: 64px;
      margin-bottom: 25px;
    }

    p {
      font-size: 22px;
      max-width: 650px;
      line-height: 1.6;
      color: #ddd;
    }

    .button {
      margin-top: 40px;
      padding: 18px 55px;
      border-radius: 50px;
      font-size: 20px;
      font-weight: bold;
      border: none;
      cursor: pointer;
      color: black;
      background: linear-gradient(135deg, gold, orange);
      box-shadow: 0 0 25px rgba(255,165,0,0.9);
    }
  </style>
</head>

<body>

  <!-- BAŞLAT EKRANI -->
  <div class="start-screen" id="startScreen">
    <h1>🎭 Gösteri Başlamak Üzere</h1>
    <button class="start-btn" id="startBtn">PERDEYİ AÇ</button>
  </div>

  <!-- PERDELER -->
  <div class="curtain left" id="leftCurtain"></div>
  <div class="curtain right" id="rightCurtain"></div>

  <div class="spotlight"></div>

  <!-- SAHNE -->
  <div class="stage" id="stage">
    <h1>Bugün Sahne Senin</h1>
    <h2>MEHTAP</h2>
    <p>
      Hayat sahnesinde yeni yaşına alkışlarla giriyorsun.  
      Bol kahkahalı, sağlık dolu ve unutulmaz anlarla dolu bir yıl seninle olsun.
    </p>

    <button class="button" id="clapBtn">👏 Alkışlar</button>
  </div>

  <!-- SESLER -->
  <audio id="curtainSound">
    <source src="https://assets.mixkit.co/sfx/preview/mixkit-theatre-curtain-open-1450.mp3" type="audio/mpeg">
  </audio>

  <audio id="applauseSound">
    <source src="https://assets.mixkit.co/sfx/preview/mixkit-audience-light-applause-354.mp3" type="audio/mpeg">
  </audio>

  <script>
    const startBtn = document.getElementById("startBtn");
    const startScreen = document.getElementById("startScreen");

    const leftCurtain = document.getElementById("leftCurtain");
    const rightCurtain = document.getElementById("rightCurtain");
    const stage = document.getElementById("stage");

    const curtainSound = document.getElementById("curtainSound");
    const applauseSound = document.getElementById("applauseSound");
    const clapBtn = document.getElementById("clapBtn");

    // ✅ TÜM SİSTEM BURADA BAŞLIYOR
    startBtn.addEventListener("click", () => {
      startScreen.style.display = "none";

      curtainSound.currentTime = 0;
      curtainSound.play();

      leftCurtain.classList.add("open");
      rightCurtain.classList.add("open");

      setTimeout(() => {
        stage.classList.add("show");
      }, 2500);
    });

    // ✅ Alkışlar %100 çalışır
    clapBtn.addEventListener("click", () => {
      applauseSound.currentTime = 0;
      applauseSound.play();
    });
  </script>

</body>
</html>
