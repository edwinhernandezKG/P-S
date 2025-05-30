<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mis Dashboards Power BI</title>
  <style>
    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      width: 100%;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #000;
      overflow: hidden;
    }

    iframe {
      position: absolute;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      border: none;
    }

    #loadingScreen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background-color: #000;
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-size: 32px;
      z-index: 9999;
      opacity: 1;
      transition: opacity 0.5s ease;
    }

    #loadingScreen.hidden {
      opacity: 0;
      pointer-events: none;
    }

    .logo {
      max-width: 200px;
      margin-bottom: 20px;
      z-index: 2;
    }

    .spinner {
      margin-top: 20px;
      border: 4px solid #ffffff30;
      border-top: 4px solid white;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      z-index: 2;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .floating-text {
      position: absolute;
      color: white;
      font-size: 42px;
      white-space: nowrap;
      animation: localOrbit 4s linear infinite;
    }

    /* Posiciones originales del texto alrededor del logo */
    .text-top {
      top: 30%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    .text-bottom {
      top: 70%;
      left: 50%;
      transform: translate(-50%, -50%);
    }

    .text-left {
      top: 50%;
      left: 25%;
      transform: translate(-50%, -50%);
    }

    .text-right {
      top: 50%;
      left: 75%;
      transform: translate(-50%, -50%);
    }

    .text-top-left {
      top: 35%;
      left: 30%;
      transform: translate(-50%, -50%);
    }

    .text-bottom-right {
      top: 65%;
      left: 70%;
      transform: translate(-50%, -50%);
    }

    /* Animación de órbita local (pequeña) */
    @keyframes localOrbit {
      0%   { transform: translate(-50%, -50%) translateX(0px) translateY(0px); }
      25%  { transform: translate(-50%, -50%) translateX(10px) translateY(-10px); }
      50%  { transform: translate(-50%, -50%) translateX(0px) translateY(-20px); }
      75%  { transform: translate(-50%, -50%) translateX(-10px) translateY(-10px); }
      100% { transform: translate(-50%, -50%) translateX(0px) translateY(0px); }
    }
  </style>
</head>
<body>
  <div id="loadingScreen">
    <img class="logo" src="https://i.ibb.co/kgSt3mNr/c947d0-eadc0d6e3f3c4184a5f64991dc4338a1-mv2-removebg-preview-1.png" alt="Logo">
    <div>Actualizando dashboard...</div>
    <div class="spinner"></div>

    <!-- Textos orbitando localmente alrededor de sus posiciones originales -->
    <div class="floating-text text-top">Más de 200 empresas</div>
    <div class="floating-text text-bottom">Diferentes medios de comunicación</div>
    <div class="floating-text text-left">Servicio 24/7 365 del año</div>
    <div class="floating-text text-right">Mesa de servicio</div>
    <div class="floating-text text-top-left">Tu tecnología en las mejores manos</div>
    <div class="floating-text text-bottom-right">Ayudando a recuperar tu experiencia</div>
  </div>

  <iframe id="dashboardFrame"></iframe>

  <script>
    const dashboards = [
      "https://app.powerbi.com/view?r=eyJrIjoiZmM4OGU2MWQtZDRhZS00YzU4LWEzMWEtMTBhMjhlYmY0MzQzIiwidCI6ImIxM2NlNGM5LTJiZTYtNDg0NC04Y2Q5LTYwOTcyMGFmYWY5YiJ9",
      "https://app.powerbi.com/view?r=eyJrIjoiNzkyYjQwZGEtNjMyYy00YjMyLTg1ZTktM2JjMWY4NGY5YTA4IiwidCI6ImIxM2NlNGM5LTJiZTYtNDg0NC04Y2Q5LTYwOTcyMGFmYWY5YiJ9",
      "https://app.powerbi.com/view?r=eyJrIjoiODk1MmFjZWYtY2IxYy00YzI0LTg5ODUtMDAzOTg1MTQ4ODMwIiwidCI6ImIxM2NlNGM5LTJiZTYtNDg0NC04Y2Q5LTYwOTcyMGFmYWY5YiJ9",
      "https://app.powerbi.com/view?r=eyJrIjoiNDMxNmU2OTUtOThhMC00NDMyLThjZmQtMmVlMTZmYWVmMDIwIiwidCI6ImIxM2NlNGM5LTJiZTYtNDg0NC04Y2Q5LTYwOTcyMGFmYWY5YiJ9",
      "https://app.powerbi.com/view?r=eyJrIjoiY2IxMGU0ZDAtNDQ5MC00Y2Y3LTk2MDItZGJmMDRjNDhhZTJjIiwidCI6ImIxM2NlNGM5LTJiZTYtNDg0NC04Y2Q5LTYwOTcyMGFmYWY5YiJ9"
    ];

    let current = 0;
    const frame = document.getElementById("dashboardFrame");
    const loadingScreen = document.getElementById("loadingScreen");

    function loadDashboard(index) {
      loadingScreen.classList.remove("hidden");

      frame.onload = () => {
        setTimeout(() => {
          loadingScreen.classList.add("hidden");
        }, 8000);
      };

      frame.src = dashboards[index] + "&cachebuster=" + new Date().getTime();
    }

    function startRotation() {
      loadDashboard(current);

      setInterval(() => {
        current = (current + 1) % dashboards.length;
        loadDashboard(current);
      }, 600000); // cada 10 minutos
    }

    startRotation();
  </script>
</body>
</html>

