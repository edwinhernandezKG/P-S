<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Integración Proactivanet & SysAid</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #f4f6f8;
    }

    .login-container, .app-container {
      max-width: 600px;
      margin: 80px auto;
      padding: 40px;
      background-color: white;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
    }

    h1, h2 {
      color: #2c3e50;
      text-align: center;
    }

    button {
      width: 100%;
      padding: 12px;
      background-color: #2c3e50;
      color: white;
      border: none;
      border-radius: 4px;
      font-size: 16px;
      cursor: pointer;
    }

    button:hover {
      background-color: #34495e;
    }

    .ticket {
      padding: 10px;
      background-color: #ecf0f1;
      border: 1px solid #bdc3c7;
      border-radius: 4px;
      margin-bottom: 10px;
      cursor: pointer;
    }

    .ticket:hover {
      background-color: #dfe6e9;
    }

    select, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 8px;
      margin-bottom: 16px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }

    #detalleTicket {
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <!-- LOGIN SIMULADO -->
  <div class="login-container" id="loginScreen">
    <h1>Bienvenido</h1>
    <p style="text-align:center;">Haz clic para acceder al panel integrado.</p>
    <button onclick="iniciarSesion()">Ingresar</button>
  </div>

  <!-- APP PRINCIPAL -->
  <div class="app-container" id="appScreen" style="display: none;">
    <h1>Panel Integrado</h1>
    <h2>Tickets Proactivanet / SysAid</h2>

    <div id="listaTickets">
      <div class="ticket" onclick="mostrarDetalle(1)">Ticket #001 - Problema de red</div>
      <div class="ticket" onclick="mostrarDetalle(2)">Ticket #002 - Error de software</div>
    </div>

    <div id="detalleTicket" style="display: none;">
      <h2>Detalle del Ticket</h2>
      <p><strong>ID SysAid:</strong> <span id="sysaidId"></span></p>
      <p><strong>ID Proactivanet:</strong> <span id="proactId"></span></p>

      <label for="estado">Estado:</label>
      <select id="estado" onchange="sincronizar('estado')">
        <option value="Abierto">Abierto</option>
        <option value="En Proceso">En Proceso</option>
        <option value="Cerrado">Cerrado</option>
      </select>

      <label for="categoria">Categoría:</label>
      <select id="categoria" onchange="sincronizar('categoria')">
        <option value="Red">Red</option>
        <option value="Software">Software</option>
        <option value="Hardware">Hardware</option>
      </select>

      <label for="evidencia">Evidencia:</label>
      <textarea id="evidencia" rows="4" onchange="sincronizar('evidencia')"></textarea>
    </div>
  </div>

  <script>
    const tickets = {
      1: {
        sysaidId: 'SYS-1001',
        proactId: 'PRO-2001',
        estado: 'Abierto',
        categoria: 'Red',
        evidencia: 'Captura de pantalla del error.'
      },
      2: {
        sysaidId: 'SYS-1002',
        proactId: 'PRO-2002',
        estado: 'En Proceso',
        categoria: 'Software',
        evidencia: 'Logs adjuntos.'
      }
    };

    function iniciarSesion() {
      document.getElementById('loginScreen').style.display = 'none';
      document.getElementById('appScreen').style.display = 'block';
    }

    function mostrarDetalle(id) {
      const ticket = tickets[id];
      document.getElementById('sysaidId').innerText = ticket.sysaidId;
      document.getElementById('proactId').innerText = ticket.proactId;
      document.getElementById('estado').value = ticket.estado;
      document.getElementById('categoria').value = ticket.categoria;
      document.getElementById('evidencia').value = ticket.evidencia;

      document.getElementById('detalleTicket').style.display = 'block';
    }

    function sincronizar(campo) {
      const valor = document.getElementById(campo).value;
      alert(`Simulación: sincronizando campo "${campo}" con valor "${valor}" en SysAid y Proactivanet`);
    }
  </script>
