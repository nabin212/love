<!DOCTYPE html> 
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Will You Be My Valentine? 💖</title>
  <!-- Google Font for handwritten letter -->
  <link href="https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap" rel="stylesheet">
  <style>
    /* ======= RESET & GLOBAL ======= */
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      background: #ff99cc;
      font-family: Arial, sans-serif;
      text-align: center;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 10px;
    }
    button { cursor: pointer; }
    
    /* ======= MAIN PAGE (YES/NO) ======= */
    #mainPage { width: 100%; }
    h1 { color: #cc0066; font-size: 2.8em; margin-bottom: 20px; }
    h2 { color: #cc0066; margin-bottom: 20px; }
    .buttons {
      position: relative;
      display: flex;
      gap: 20px;
      justify-content: center;
    }
    .valentine-btn {
      padding: 15px 30px;
      font-size: 1.3em;
      border: none;
      border-radius: 10px;
      transition: transform 0.3s;
      box-shadow: 0 3px 6px rgba(0,0,0,0.15);
    }
    #yesBtn { background-color: #4CAF50; color: white; }
    /* Reverting to original behavior: absolute positioning with an initial position so they don't overlap */
    #noBtn { background-color: #f44336; color: white; position: absolute; left: 70%; top: 50%; }
    
    /* ======= INTERACTIVE PAGE ======= */
    #interactivePage {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      background: #ffccff;
      width: 100%;
      min-height: 100vh;
      padding: 20px;
      box-sizing: border-box;
    }
    #interactivePage h1 { margin-top: 20px; color: #ff0066; }
    .menu-buttons { margin-bottom: 20px; }
    .menu-buttons button {
      padding: 10px 20px;
      font-size: 1.1em;
      border: none;
      border-radius: 8px;
      margin: 10px;
      color: #fff;
      box-shadow: 0 3px 6px rgba(0,0,0,0.15);
    }
    #heartsBtn { background-color: #e91e63; }
    #letterBtn { background-color: #3f51b5; }
    #content {
      margin-top: 20px;
      width: 100%;
      max-width: 600px;
      min-height: 300px;
      position: relative;
      border: 1px solid #ccc;
      border-radius: 8px;
      background: #ffe6f2;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
      overflow: hidden;
      padding: 10px;
    }
    
    /* ======= HEART SECTION WITH BUTTERFLIES ======= */
    #heartAnimationContainer {
      position: relative;
      width: 300px;
      height: 300px;
      margin: 20px auto;
      /* A subtle beat effect */
      animation: beat 1.4s infinite;
    }
    @keyframes beat {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }
    /* Center heart (SVG) */
    .center-heart {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 250px;
      height: 250px;
      transform: translate(-50%, -50%);
    }
    .center-heart svg { width: 100%; height: 100%; }
    /* Butterfly style – using a fixed butterfly image URL */
    .butterfly {
      position: absolute;
      width: 30px;
      height: 30px;
      transition: transform 0.7s ease;
      filter: drop-shadow(1px 1px 3px rgba(0,0,0,0.3));
    }
    
    /* ======= LOVE LETTER (NOTEBOOK STYLE) ======= */
    .loveLetterContainer {
      width: 90%;
      max-width: 350px;
      margin: 20px auto;
      padding: 20px;
      background: #fff;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.15);
      background-image: repeating-linear-gradient(
        to bottom,
        transparent,
        transparent 24px,
        #f0f0f0 25px
      );
      position: relative;
      overflow: hidden;
    }
    .loveLetterContainer p {
      font-family: 'Indie Flower', cursive;
      font-size: 1.6em;
      color: #333;
      line-height: 1.4;
      margin: 10px 0;
    }
    /* Animated icons for added romance */
    .animatedIcons {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
    }
    .animatedIcons span {
      position: absolute;
      font-size: 1.5em;
      opacity: 0;
      animation: floatIn 3s ease-in-out infinite;
    }
    @keyframes floatIn {
      0%   { transform: translateY(50px) scale(0.5); opacity: 0; }
      50%  { opacity: 1; }
      100% { transform: translateY(-50px) scale(1); opacity: 0; }
    }
    
    /* ======= RESPONSIVE ADJUSTMENTS ======= */
    @media (max-width: 480px) {
      h1 { font-size: 2em; }
      .valentine-btn { font-size: 1.1em; padding: 10px 20px; }
      .loveLetterContainer { max-width: 90%; padding: 15px; }
    }
  </style>
</head>
<body>
  <!-- MAIN PAGE -->
  <div id="mainPage">
    <h1>🌹 Happy Valentine's Day! 🌹</h1>
    <h2>Will you be my Valentine?</h2>
    <div class="buttons">
      <button id="yesBtn" class="valentine-btn" onclick="showLove()">Yes! 💖</button>
      <button id="noBtn" class="valentine-btn" onmouseover="moveButton()">No</button>
    </div>
  </div>
  
  <!-- INTERACTIVE PAGE -->
  <div id="interactivePage">
    <h1>Thank you, my dear love! 💖</h1>
    <div class="menu-buttons">
      <button id="heartsBtn" onclick="showHearts()">Hearts 💕</button>
      <button id="letterBtn" onclick="showLoveLetter()">Love Letter 💌</button>
    </div>
    <div id="content"></div>
  </div>
  
  <script>
    // Move the "No" button randomly when hovered
    function moveButton() {
      const noBtn = document.getElementById('noBtn');
      const x = Math.random() * (window.innerWidth - noBtn.offsetWidth);
      const y = Math.random() * (window.innerHeight - noBtn.offsetHeight);
      noBtn.style.left = x + 'px';
      noBtn.style.top = y + 'px';
    }
    
    // Switch from main page to interactive page
    function showLove() {
      document.getElementById('mainPage').style.display = 'none';
      document.getElementById('interactivePage').style.display = 'flex';
    }
    
    // Utility: clear content area
    function clearContent() {
      document.getElementById('content').innerHTML = '';
    }
    
    /* ---------- HEARTS FEATURE: Heart Covered with Butterflies ---------- */
    function showHearts() {
      clearContent();
      const container = document.createElement('div');
      container.id = 'heartAnimationContainer';
      container.style.position = 'relative';
      container.style.width = '300px';
      container.style.height = '300px';
      container.style.margin = 'auto';
      container.style.animation = 'beat 1.4s infinite';
      
      // Add a centered, beating heart (SVG)
      const centerHeart = document.createElement('div');
      centerHeart.className = 'center-heart';
      centerHeart.innerHTML = `
        <svg viewBox="0 0 200 200">
          <defs>
            <linearGradient id="bigHeartGrad" x1="0%" y1="0%" x2="100%" y2="0%">
              <stop offset="0%" stop-color="#ff5f7e"/>
              <stop offset="100%" stop-color="#ff99ac"/>
            </linearGradient>
          </defs>
          <path fill="url(#bigHeartGrad)" d="M100 180 L40 120 A40 40 0 1 1 100 60 A40 40 0 1 1 160 120 Z"/>
        </svg>
      `;
      container.appendChild(centerHeart);
      
      // Add the name "Roshini" at the center of the heart
      const heartName = document.createElement('div');
      heartName.textContent = "Roshini";
      heartName.style.position = "absolute";
      heartName.style.top = "50%";
      heartName.style.left = "50%";
      heartName.style.transform = "translate(-50%, -50%)";
      heartName.style.fontFamily = "'Indie Flower', cursive";
      heartName.style.fontSize = "2em";
      heartName.style.color = "#ff5f7e";
      container.appendChild(heartName);
      
      // Arrange many butterflies along the heart outline
      const totalButterflies = 60;
      const scaleFactor = 5;
      const centerX = 300 / 2, centerY = 300 / 2;
      
      for (let i = 0; i < totalButterflies; i++) {
        // Evenly space t in [0, 2pi]
        let t = (i / totalButterflies) * 2 * Math.PI;
        let x = 16 * Math.pow(Math.sin(t), 3);
        let y = 13 * Math.cos(t) - 5 * Math.cos(2*t) - 2 * Math.cos(3*t) - Math.cos(4*t);
        x *= scaleFactor;
        y *= scaleFactor;
        const posX = centerX + x;
        const posY = centerY - y;
        
        const butterfly = document.createElement('img');
        butterfly.className = 'butterfly';
        // Hard-coded butterfly image
        butterfly.src = 'https://em-content.zobj.net/source/apple/391/butterfly_1f98b.png';
        butterfly.style.left = posX + 'px';
        butterfly.style.top = posY + 'px';
        butterfly.dataset.origX = posX;
        butterfly.dataset.origY = posY;
        container.appendChild(butterfly);
      }
      
      // On hover, scatter the butterflies; on mouse leave, reset their positions
      container.addEventListener('mouseenter', () => {
        const butterflies = container.querySelectorAll('.butterfly');
        butterflies.forEach(b => {
          const offsetX = (Math.random() - 0.5) * 100;
          const offsetY = (Math.random() - 0.5) * 100;
          const angle = Math.random() * 360;
          b.style.transform = `translate(${offsetX}px, ${offsetY}px) rotate(${angle}deg)`;
        });
      });
      container.addEventListener('mouseleave', () => {
        const butterflies = container.querySelectorAll('.butterfly');
        butterflies.forEach(b => {
          b.style.transform = 'translate(0,0) rotate(0deg)';
        });
      });
      
      document.getElementById('content').appendChild(container);
    }
    
    /* ---------- LOVE LETTER FEATURE: Notebook-Style Letter with Animated Icons ---------- */
    function showLoveLetter() {
      clearContent();
      const container = document.createElement('div');
      container.className = 'loveLetterContainer';
      container.innerHTML = `
        <p>My dearest,</p>
        <p>Your love fills every page of my heart like the gentle scribbles of a cherished notebook.</p>
        <p>Each moment with you writes a verse in the sweetest poem.</p>
        <p>Forever in love,</p>
        <p>A Soul in Love</p>
        <div class="animatedIcons"></div>
      `;
      
      // Add animated icons (hearts and flowers) that float in
      const iconsContainer = container.querySelector('.animatedIcons');
      const icons = ['❤️', '🌸'];
      for (let i = 0; i < 6; i++) {
        const icon = document.createElement('span');
        icon.innerText = icons[i % icons.length];
        icon.style.left = (Math.random() * 80 + 10) + '%';
        icon.style.top = (Math.random() * 80 + 10) + '%';
        icon.style.animationDelay = Math.random() * 2 + 's';
        iconsContainer.appendChild(icon);
      }
      
      document.getElementById('content').appendChild(container);
    }
  </script>
</body>
</html>
