<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Para mi niña bonita 💗</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      min-height: 100dvh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: "Segoe UI", sans-serif;
      background: linear-gradient(135deg, #ffe0ec, #ffc2d8, #fff0f5);
      color: #a83263;
      overflow: hidden;
      padding: 20px;
    }

    .card {
      width: 100%;
      max-width: 430px;
      padding: 30px 22px;
      background: rgba(255, 255, 255, 0.8);
      border: 2px solid #fff;
      border-radius: 28px;
      box-shadow: 0 12px 35px rgba(200, 70, 120, 0.2);
      text-align: center;
      position: relative;
      z-index: 1;
    }

    .screen {
      display: none;
      animation: appear 0.5s ease;
    }

    .screen.active {
      display: block;
    }

    @keyframes appear {
      from {
        opacity: 0;
        transform: translateY(12px);
      }
      to {
        opacity: 1;
        transform: translateY(0);
      }
    }

    h1 {
      font-size: 29px;
      margin: 10px 0 18px;
      color: #d63384;
    }

    h2 {
      font-size: 27px;
      line-height: 1.5;
      color: #d63384;
    }

    p {
      font-size: 16px;
      line-height: 1.7;
    }

    .heart {
      font-size: 55px;
      margin: 15px 0;
      animation: heartbeat 1.2s infinite;
    }

    @keyframes heartbeat {
      0%, 100% {
        transform: scale(1);
      }
      50% {
        transform: scale(1.12);
      }
    }

    button {
      border: none;
      border-radius: 30px;
      padding: 13px 20px;
      font-size: 16px;
      font-weight: bold;
      cursor: pointer;
      font-family: inherit;
      -webkit-tap-highlight-color: transparent;
    }

    .next {
      background: #e75480;
      color: white;
      margin-top: 12px;
      box-shadow: 0 5px 12px rgba(231, 84, 128, 0.25);
    }

    .next:hover {
      background: #d6336c;
    }

    .buttons {
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 15px;
      min-height: 110px;
      margin-top: 25px;
      overflow: visible;
    }

    .yes {
      background: #35b86b;
      color: white;
      box-shadow: 0 5px 12px rgba(53, 184, 107, 0.25);
      position: relative;
      z-index: 3;
      flex-shrink: 0;

      /* Crece desde su centro sin cambiar de lugar */
      transform: scale(1);
      transform-origin: center center;
      transition: transform 0.25s ease;
    }

    .no {
      background: #f2a5bb;
      color: #7c2444;
      position: relative;
      z-index: 10;
      flex-shrink: 0;
      transition: left 0.18s ease, top 0.18s ease;
    }

    .caption {
      min-height: 25px;
      font-size: 15px;
      color: #b34470;
    }

    .signature {
      margin-top: 24px;
      font-weight: bold;
      color: #d63384;
    }

    .floating-heart {
      position: fixed;
      bottom: -40px;
      font-size: 24px;
      pointer-events: none;
      z-index: 20;
      animation: floatUp 5s linear forwards;
    }

    @keyframes floatUp {
      from {
        transform: translateY(0) rotate(0deg);
        opacity: 1;
      }
      to {
        transform: translateY(-110vh) rotate(360deg);
        opacity: 0;
      }
    }

    @media (max-width: 380px) {
      .card {
        padding: 25px 15px;
      }

      h2 {
        font-size: 24px;
      }

      .buttons {
        gap: 10px;
      }

      button {
        padding: 12px 15px;
        font-size: 15px;
      }
    }
  </style>
</head>

<body>
  <main class="card">

    <!-- SCREEN 1 -->
    <section class="screen active" id="screen1">
      <h1>Para mi niña bonita</h1>
      <div class="heart">💗</div>
      <p>De José, para alguien muy especial...</p>
      <p>Ximena, tengo algo que preguntarte... 💕</p>
      <button class="next" onclick="goToScreen(2)">
        Tengo curiosidad 💌
      </button>
    </section>

    <!-- SCREEN 2 -->
    <section class="screen" id="screen2">
      <div class="heart">💖</div>

      <h2>
        MI AMOR
        <br>
        ¿QUIERES SER MI NOVIA?
      </h2>

      <p>Prometo hacerte sonreír y darte mucho cariño. 💕</p>
      <p class="caption" id="caption">Piénsalo bien, mi amor 💗</p>

      <div class="buttons" id="buttonArea">
        <button class="yes" id="yesBtn" onclick="sayYes()">
          ¡SÍ, QUIERO! 💗
        </button>

        <button class="no" id="noBtn" onclick="noClicked()">
          No
        </button>
      </div>
    </section>

    <!-- SCREEN 3 -->
    <section class="screen" id="screen3">
      <h1>¡Sabía que dirías que sí!</h1>

      <p>
        Mi amor, me haces muy feliz.
        Espero que podamos compartir muchos momentos bonitos,
        reír juntos y crear recuerdos inolvidables. 💕
      </p>

      <p>Gracias por darme esta oportunidad, mi niña bonita.</p>

      <div class="heart">💗</div>
      <p class="signature">Con cariño, tu novio. 💌</p>
    </section>

  </main>

  <script>
    let attempts = 0;
    let yesScale = 1;
    let noIsMoving = false;

    const yes = document.getElementById("yesBtn");
    const no = document.getElementById("noBtn");
    const caption = document.getElementById("caption");

    function goToScreen(number) {
      document.querySelectorAll(".screen").forEach(screen => {
        screen.classList.remove("active");
      });

      document.getElementById("screen" + number).classList.add("active");

      // Reinicia la posición del NO al entrar en la segunda pantalla.
      if (number === 2) {
        resetNoButton();
      }
    }

    const reactions = [
      "¿Segura que no, mi amor? 💗",
      "Ándale, mi amorcito... 💕",
      "Me estás rompiendo el corazón...",
      "Mi corazoncito no aguanta 😭",
      "Mira que el sí se está haciendo grande...",
      "Por favorcito, mi amor 💗",
      "Ándale, di que sí jajaja 💞"
    ];

    function resetNoButton() {
      noIsMoving = false;
      no.style.position = "relative";
      no.style.left = "";
      no.style.top = "";
      no.style.transform = "";
      no.textContent = "No";
      attempts = 0;
      yesScale = 1;
      yes.style.transform = "scale(1)";
      caption.textContent = "Piénsalo bien, mi amor 💗";
    }

    function noClicked() {
      attempts++;

      // El SÍ crece en cada intento desde su propio centro.
      yesScale += 0.18;
      yes.style.transform = `scale(${yesScale})`;

      // Carita triste y paréntesis acumulados.
      no.textContent = "No :(" + "(".repeat(attempts - 1);

      caption.textContent =
        reactions[Math.min(attempts - 1, reactions.length - 1)];

      // Saca el botón del contenedor y lo mueve por toda la pantalla.
      moveNoAcrossScreen();
    }

    function moveNoAcrossScreen() {
      // Usa coordenadas de la pantalla completa, no de la tarjeta.
      noIsMoving = true;

      const margin = 12;
      const buttonWidth = no.offsetWidth;
      const buttonHeight = no.offsetHeight;

      const maxX = Math.max(
        margin,
        window.innerWidth - buttonWidth - margin
      );

      const maxY = Math.max(
        margin,
        window.innerHeight - buttonHeight - margin
      );

      let x;
      let y;

      const oldX = parseFloat(no.style.left);
      const oldY = parseFloat(no.style.top);

      // Busca un lugar distinto al anterior.
      let tries = 0;

      do {
        x = margin + Math.random() * (maxX - margin);
        y = margin + Math.random() * (maxY - margin);
        tries++;
      } while (
        tries < 30 &&
        Number.isFinite(oldX) &&
        Number.isFinite(oldY) &&
        Math.abs(x - oldX) < 100 &&
        Math.abs(y - oldY) < 70
      );

      // position: fixed permite moverse por toda la ventana.
      no.style.position = "fixed";
      no.style.left = x + "px";
      no.style.top = y + "px";
      no.style.transform = "none";
    }

    // Si cambia el tamaño de la ventana, mantiene el botón visible.
    window.addEventListener("resize", () => {
      if (noIsMoving) {
        const margin = 12;

        const maxX = Math.max(
          margin,
          window.innerWidth - no.offsetWidth - margin
        );

        const maxY = Math.max(
          margin,
          window.innerHeight - no.offsetHeight - margin
        );

        const currentX = parseFloat(no.style.left) || margin;
        const currentY = parseFloat(no.style.top) || margin;

        no.style.left = Math.min(currentX, maxX) + "px";
        no.style.top = Math.min(currentY, maxY) + "px";
      }
    });

    function sayYes() {
      noIsMoving = false;
      goToScreen(3);
      hearts();
    }

    function hearts() {
      const emojis = ["💗", "💖", "💕", "💘", "💝", "❤️"];

      for (let i = 0; i < 35; i++) {
        setTimeout(() => {
          const heart = document.createElement("div");

          heart.className = "floating-heart";
          heart.textContent =
            emojis[Math.floor(Math.random() * emojis.length)];

          heart.style.left = Math.random() * 100 + "vw";
          heart.style.animationDuration =
            (3 + Math.random() * 3) + "s";

          document.body.appendChild(heart);

          setTimeout(() => heart.remove(), 6000);
        }, i * 100);
      }
    }
  </script>
</body>
</html>
