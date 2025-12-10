<html lang="tr" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dijital Kutlama Kartı</title>
  <script src="/_sdk/element_sdk.js"></script>
  <style>
    body {
      box-sizing: border-box;
    }
    
    * {
      box-sizing: border-box;
    }
    
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
    }
    
    .card-wrapper {
      width: 100%;
      height: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      background: linear-gradient(135deg, #E8B4F0 0%, #B8D4F1 100%);
      position: relative;
    }
    
    .card-container {
      background: white;
      border-radius: 24px;
      padding: 48px;
      box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
      max-width: 500px;
      width: 90%;
      text-align: center;
      position: relative;
      z-index: 10;
      transform: scale(0.95);
      transition: transform 0.3s ease;
    }
    
    .card-container.active {
      transform: scale(1);
    }
    
    .recipient-name {
      font-size: 48px;
      font-weight: bold;
      color: #D946EF;
      margin: 24px 0;
      font-family: 'Georgia', serif;
    }
    
    .main-message {
      font-size: 32px;
      font-weight: 600;
      color: #1E293B;
      margin: 16px 0;
      font-family: 'Arial', sans-serif;
    }
    
    .personal-message {
      font-size: 18px;
      color: #64748B;
      margin: 24px 0;
      line-height: 1.6;
      font-family: 'Arial', sans-serif;
    }
    
    .celebrate-button {
      background: linear-gradient(135deg, #D946EF 0%, #60A5FA 100%);
      color: white;
      border: none;
      border-radius: 50px;
      padding: 16px 48px;
      font-size: 18px;
      font-weight: 600;
      cursor: pointer;
      margin-top: 24px;
      box-shadow: 0 8px 16px rgba(217, 70, 239, 0.3);
      transition: all 0.3s ease;
      font-family: 'Arial', sans-serif;
    }
    
    .celebrate-button:hover {
      transform: translateY(-2px);
      box-shadow: 0 12px 24px rgba(217, 70, 239, 0.4);
    }
    
    .celebrate-button:active {
      transform: translateY(0);
    }
    
    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      pointer-events: none;
    }
    
    .balloon {
      position: absolute;
      bottom: -100px;
      animation: float-up 8s ease-in-out infinite;
    }
    
    @keyframes float-up {
      0% {
        transform: translateY(0) rotate(0deg);
        opacity: 1;
      }
      100% {
        transform: translateY(-120vh) rotate(360deg);
        opacity: 0;
      }
    }
    
    @keyframes confetti-fall {
      0% {
        transform: translateY(-20px) rotate(0deg);
        opacity: 1;
      }
      100% {
        transform: translateY(120vh) rotate(720deg);
        opacity: 0;
      }
    }
    
    .decoration-icon {
      display: inline-block;
      font-size: 32px;
      margin: 0 8px;
      animation: bounce 2s ease-in-out infinite;
    }
    
    @keyframes bounce {
      0%, 100% {
        transform: translateY(0);
      }
      50% {
        transform: translateY(-10px);
      }
    }
  </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body class="h-full">
  <div class="card-wrapper" id="cardWrapper">
   <div class="card-container" id="cardContainer">
    <div class="decoration-icon">
     🎉
    </div>
    <div class="decoration-icon">
     🎈
    </div>
    <div class="decoration-icon">
     🎊
    </div>
    <h1 class="main-message" id="mainMessage">Doğum Günün Kutlu Olsun!</h1>
    <h2 class="recipient-name" id="recipientName">Pelin</h2>
    <p class="personal-message" id="personalMessage">Bu özel günde mutluluk ve sağlık dolu bir yıl geçirmen dileğiyle. En güzel dileklerimle! 🌟</p><button class="celebrate-button" id="celebrateBtn"> Kutlamayı Başlat 🎉 </button>
   </div>
  </div>
  <script>
    const defaultConfig = {
      recipient_name: "Pelin",
      main_message: "Doğum Günün Kutlu Olsun!",
      personal_message: "Bu özel günde mutluluk ve sağlık dolu bir yıl geçirmen dileğiyle. En güzel dileklerimle! 🌟",
      background_gradient_start: "#E8B4F0",
      background_gradient_end: "#B8D4F1",
      primary_color: "#D946EF",
      text_color: "#1E293B",
      secondary_text_color: "#64748B"
    };

    async function onConfigChange(config) {
      const recipientName = config.recipient_name || defaultConfig.recipient_name;
      const mainMessage = config.main_message || defaultConfig.main_message;
      const personalMessage = config.personal_message || defaultConfig.personal_message;
      const bgGradientStart = config.background_gradient_start || defaultConfig.background_gradient_start;
      const bgGradientEnd = config.background_gradient_end || defaultConfig.background_gradient_end;
      const primaryColor = config.primary_color || defaultConfig.primary_color;
      const textColor = config.text_color || defaultConfig.text_color;
      const secondaryTextColor = config.secondary_text_color || defaultConfig.secondary_text_color;
      
      document.getElementById('recipientName').textContent = recipientName;
      document.getElementById('mainMessage').textContent = mainMessage;
      document.getElementById('personalMessage').textContent = personalMessage;
      
      document.querySelector('.card-wrapper').style.background = `linear-gradient(135deg, ${bgGradientStart} 0%, ${bgGradientEnd} 100%)`;
      document.querySelector('.recipient-name').style.color = primaryColor;
      document.querySelector('.main-message').style.color = textColor;
      document.querySelector('.personal-message').style.color = secondaryTextColor;
      
      const button = document.querySelector('.celebrate-button');
      button.style.background = `linear-gradient(135deg, ${primaryColor} 0%, ${bgGradientEnd} 100%)`;
    }

    function createConfetti() {
      const colors = ['#D946EF', '#60A5FA', '#F472B6', '#A78BFA', '#34D399'];
      const shapes = ['circle', 'square', 'triangle'];
      
      for (let i = 0; i < 50; i++) {
        const confetti = document.createElement('div');
        confetti.className = 'confetti';
        confetti.style.left = Math.random() * 100 + '%';
        confetti.style.top = '-20px';
        confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
        confetti.style.animation = `confetti-fall ${2 + Math.random() * 3}s ease-out ${Math.random() * 0.5}s`;
        confetti.style.animationFillMode = 'forwards';
        
        if (shapes[Math.floor(Math.random() * shapes.length)] === 'circle') {
          confetti.style.borderRadius = '50%';
        }
        
        document.getElementById('cardWrapper').appendChild(confetti);
        
        setTimeout(() => {
          confetti.remove();
        }, 5000);
      }
    }

    function createBalloons() {
      const balloonColors = ['#D946EF', '#60A5FA', '#F472B6', '#34D399'];
      
      for (let i = 0; i < 5; i++) {
        const balloon = document.createElementNS('http://www.w3.org/2000/svg', 'svg');
        balloon.setAttribute('class', 'balloon');
        balloon.setAttribute('width', '40');
        balloon.setAttribute('height', '60');
        balloon.style.left = (i * 20 + Math.random() * 10) + '%';
        balloon.style.animationDelay = (Math.random() * 2) + 's';
        balloon.style.animationDuration = (6 + Math.random() * 4) + 's';
        
        const color = balloonColors[Math.floor(Math.random() * balloonColors.length)];
        
        balloon.innerHTML = `
          <ellipse cx="20" cy="25" rx="15" ry="20" fill="${color}" opacity="0.9"/>
          <line x1="20" y1="45" x2="20" y2="60" stroke="${color}" stroke-width="1"/>
        `;
        
        document.getElementById('cardWrapper').appendChild(balloon);
        
        setTimeout(() => {
          balloon.remove();
        }, 10000);
      }
    }

    document.getElementById('celebrateBtn').addEventListener('click', function(e) {
      e.preventDefault();
      createConfetti();
      createBalloons();
      document.getElementById('cardContainer').classList.add('active');
      
      setTimeout(() => {
        document.getElementById('cardContainer').classList.remove('active');
      }, 300);
    });

    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig,
        onConfigChange,
        mapToCapabilities: (config) => ({
          recolorables: [
            {
              get: () => config.background_gradient_start || defaultConfig.background_gradient_start,
              set: (value) => {
                config.background_gradient_start = value;
                window.elementSdk.setConfig({ background_gradient_start: value });
              }
            },
            {
              get: () => config.background_gradient_end || defaultConfig.background_gradient_end,
              set: (value) => {
                config.background_gradient_end = value;
                window.elementSdk.setConfig({ background_gradient_end: value });
              }
            },
            {
              get: () => config.primary_color || defaultConfig.primary_color,
              set: (value) => {
                config.primary_color = value;
                window.elementSdk.setConfig({ primary_color: value });
              }
            },
            {
              get: () => config.text_color || defaultConfig.text_color,
              set: (value) => {
                config.text_color = value;
                window.elementSdk.setConfig({ text_color: value });
              }
            },
            {
              get: () => config.secondary_text_color || defaultConfig.secondary_text_color,
              set: (value) => {
                config.secondary_text_color = value;
                window.elementSdk.setConfig({ secondary_text_color: value });
              }
            }
          ],
          borderables: [],
          fontEditable: undefined,
          fontSizeable: undefined
        }),
        mapToEditPanelValues: (config) => new Map([
          ["recipient_name", config.recipient_name || defaultConfig.recipient_name],
          ["main_message", config.main_message || defaultConfig.main_message],
          ["personal_message", config.personal_message || defaultConfig.personal_message]
        ])
      });
    }

    setTimeout(() => {
      document.getElementById('cardContainer').classList.add('active');
    }, 100);
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9abb69e5c32126ad',t:'MTc2NTM1NTc3Ny4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>

  body {
<audio id="confettiSound" preload="auto">
  <source src="https://assets.mixkit.co/sfx/preview/mixkit-party-popper-burst-252.mp3" type="audio/mpeg">
</audio>
