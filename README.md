<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mis Dashboards Power BI</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      height: 100%;
    }

    iframe {
      width: 100%;
      height: 100%;
      border: none;
      display: block;
    }

    #loadingScreen {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: black;
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      z-index: 9999;
      opacity: 1;
      transition: opacity 0.3s ease;
    }

    #loadingScreen.hidden {
      opacity: 0;
      pointer-events: none;
    }
  </style>
</head>
<body>
  <div id="loadingScreen">Cargando dashboard...</div>
  <iframe id="dashboardFrame"></iframe>

  <script>
    const dashboards = [
      "https://app.powerbi.com/view?r=eyJrIjoiY2IxMGU0ZDAtNDQ5MC00Y2Y3LTk2MDItZGJmMDRjNDhhZTJjIiwidCI6ImIxM2NlNGM5LTJiZTYtNDg0NC04Y2Q5LTYwOTcyMGFmYWY5YiJ9",
      "https://app.powerbi.com/view?r=eyJrIjoiODk1MmFjZWYtY2IxYy00YzI0LTg5ODUtMDAzOTg1MTQ4ODMwIiwidCI6ImIxM2NlNGM5LTJiZTYtNDg0NC04Y2Q5LTYwOTcyMGFmYWY5YiJ9"
    ];

    let current = 0;
    const frame = document.getElementById("dashboardFrame");
    const loadingScreen = document.getElementById("loadingScreen");

    function loadDashboard(index) {
      loadingScreen.classList.remove("hidden"); // Mostrar pantalla negra

      frame.onload = () => {
        // Mantener la pantalla negra visible por 8 segundos
        setTimeout(() => {
          loadingScreen.classList.add("hidden");
        }, 8000);
      };

      frame.src = dashboards[index] + "&cachebuster=" + new Date().getTime();
    }

    // Cargar el primer dashboard
    loadDashboard(current);

    setInterval(() => {
      current = (current + 1) % dashboards.length;
      loadDashboard(current);
    }, 20000); // Cambiar cada 20 segundos (8 de carga + 12 de visualización)
  </script>
</body>
</html>

