Siguiente HTML pero que la pantalla en negro que pasa cuando cambia de dashboar dure 6 segundos

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
      font-size: 30px;
      z-index: 9999;
      opacity: 1;
      transition: opacity 0.5s ease;
    }

    #loadingScreen.hidden {
      opacity: 0;
      pointer-events: none;
    }

    .logo {
      max-width: 160px;
      margin-bottom: 1px;
      border: none;
      outline: none;
    }

    .spinner {
      margin-top: 20px;
      border: 4px solid #ffffff30;
      border-top: 4px solid white;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
  </style>
</head>
<body>
  <div id="loadingScreen">
    <img class="logo" src="https://i.ibb.co/kgSt3mNr/c947d0-eadc0d6e3f3c4184a5f64991dc4338a1-mv2-removebg-preview-1.png" alt="Logo">
    <div>Actualizando dashboard...</div>
    <div class="spinner"></div>
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
        }, 8000); // Mostrar pantalla de carga por 8 segundos
      };

      frame.src = dashboards[index] + "&cachebuster=" + new Date().getTime();
    }

    function startRotation() {
      loadDashboard(current);

      setInterval(() => {
        current = (current + 1) % dashboards.length;
        loadDashboard(current);
      }, 600000); // Cada 10 minutos
    }

    startRotation();
  </script>
</body>
</html>
