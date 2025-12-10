<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>Sahne Senin</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: "Georgia", serif;
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

    /* PERDE */
    .curtain {
      position: fixed;
      top: 0;
      width: 50%;
      height: 100%;
      background: linear-gradient(135deg, #7a0000, #b30000);
      z-index: 10;
      transition: transform 2.2s ease-in-out;
    }

    .curtain.left {
      left: 0;
    }

    .curtain.right {
      right: 0;
    }

    .curtain.open.left {
      transform: translateX(-100%);
    }

    .curtain.open.right {
      transform: translateX(100%);
    }

    /* SAHNE */
    .stage {
      text-align: center;
      opacity: 0;
      transform: scale(0.9);
      transition: 2s ease;
      z-index: 1;
    }

    .stage.show {
      opacity: 1;
      transform: scale(1);
    }

    .spotlight {
      position: absolute;
      top: -20%;
      left: 50%;
      width: 300px;
      height: 800px;
      transform: translateX(-50%);
      background: radial-gradient(circle at top, rgba(255,255,255,0.5), transparent 70%);
      filter: blur(10px);
      animation: lightMove 5s infinite alternate;
      z-index: 0;
    }

    @keyframes lightMove {
      from { transform: translateX(-60%); }
      to { transform: translateX(-40%); }
    }

    h1 {
      font-size: 48px;
      color: gold;
      text-shadow: 0 0 20px rgba(255,215,0,0.6);
      margin-bottom: 20px;
      letter-spacing: 2px;
      animation: glow 2s infinite alternate;
    }

    @keyframes glow {
      from { text-shadow: 0 0 10px rgba(255,215,0,0.4); }
      to { text-shadow: 0 0 25px rgba(255,215,0,1); }
    }

    h2 {
      font-size: 64px;
      margin-bottom: 20px;
    }

    p {
      font-size: 22px;
      max-width: 600px;
      line-height: 1.6;
      color: #ddd;
    }

    .button {
      margin-top: 40px;
      padding: 18px 50px;
      border-radius: 50px;
      font-size: 20px;
      font-weight: bold;
      border: none;
      cursor: pointer;
      color: black;
      background: linear-gradient(135deg, gold, orange);
      box-shadow: 0 0 20px rgba(255,165,0,0.8);
      transition: 0.3s;
    }

    .button:hover {
      transform: scale(1.05);
      box-shadow: 0 0 40px rgba(255,165,0,1);
    }
  </style>
</head>

<body>

  <!-- PERDELER -->
  <div class="curtain left" id="leftCurtain"></div>
  <div class="curtain right" id="rightCurtain"></div>

  <!-- SPOT IŞIĞI -->
  <div class="spotlight"></div>

  <!-- SAHNE -->
  <div class="stage" id="stage">
    <h1>🎭 Bugün Sahne Senin 🎭</h1>
    <h2>MEHTAP</h2>
    <p>
      Hayat sahnesinde yeni yaşına alkışlarla giriyorsun.  
      Bol kahkahalı, sağlık dolu ve unutulmaz anlarla dolu bir yıl seninle olsun.
    </p>

    <button class="button" id="clapBtn">👏 Alkışlar Başlasın</button>
  </div>

  <!-- SESLER -->
  <audio id="curtainSound">
    <source src="https://assets.mixkit.co/sfx/preview/mixkit-theatre-curtain-open-1450.mp3" type="audio/mpeg">
  </audio>

  <audio id="applauseSound">
    <source src="https://assets.mixkit.co/sfx/preview/mixkit-audience-light-applause-354.mp3" type="audio/mpeg">
  </audio>

  <!-- SCRIPT -->
  <script>
    const leftCurtain = document.getElementById("leftCurtain");
    const rightCurtain = document.getElementById("rightCurtain");
    const stage = document.getElementById("stage");
    const curtainSound = document.getElementById("curtainSound");
    const applauseSound = document.getElementById("applauseSound");
    const clapBtn = document.getElementById("clapBtn");

    // Sayfa açılınca perde açılıyor
    window.onload = () => {
      setTimeout(() => {
        curtainSound.play();
        leftCurtain.classList.add("open");
        rightCurtain.classList.add("open");
      }, 800);

      setTimeout(() => {
        stage.classList.add("show");
      }, 2600);
    };

    // Alkış butonu
    clapBtn.addEventListener("click", () => {
      applauseSound.currentTime = 0;
      applauseSound.play();
    });
  </script>

</body>
</html>
