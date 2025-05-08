<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Integración SysAid ↔ Proactivanet</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f6f8;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 30px;
    }

    .container {
      display: flex;
      justify-content: space-around;
      align-items: flex-start;
      width: 90%;
      margin-top: 40px;
      gap: 40px;
    }

    .box {
      background: white;
      padding: 20px;
      border-radius: 10px;
      width: 300px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    .box h2 {
      text-align: center;
      color: #0077b6;
    }

    .arrow {
      font-size: 50px;
      color: #00b4d8;
      margin-top: 100px;
    }

    .log {
      margin-top: 30px;
      background: #e9ecef;
      padding: 10px;
      border-radius: 8px;
      font-family: monospace;
      height: 180px;
      width: 90%;
      overflow-y: auto;
    }

    button {
      margin: 5px 0;
      padding: 8px 12px;
      background: #0077b6;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      width: 100%;
    }

    button:hover {
      background: #023e8a;
    }

    .label {
      font-weight: bold;
    }
  </style>
</head>
<body>

  <h1>Integración bidireccional entre SysAid y Proactivanet</h1>
  <p>Simulación de estado y categoría sincronizados por API.</p>

  <div class="container">
    <!-- SysAid -->
    <div class="box" id="sysaid">
      <h2>SysAid</h2>
      <p><span class="label">Status:</span> <span id="statusSysAid">Abierto</span></p>
      <p><span class="label">Categoría:</span> <span id="catSysAid">Redes</span></p>
      <p><span class="label">Documentación:</span> adjunto.pdf</p>

      <button onclick="updateFromSysAid('Cerrado')">Cambiar a Cerrado</button>
      <button onclick="updateFromSysAid('Abierto')">Cambiar a Abierto</button>

      <button onclick="updateCatFromSysAid('Redes')">Categoría: Redes</button>
      <button onclick="updateCatFromSysAid('Soporte')">Categoría: Soporte</button>
      <button onclick="updateCatFromSysAid('Hardware')">Categoría: Hardware</button>
    </div>

    <div class="arrow">⇄</div>

    <!-- Proactivanet -->
    <div class="box" id="proactivanet">
      <h2>Proactivanet</h2>
      <p><span class="label">Status:</span> <span id="statusProactiva">Abierto</span></p>
      <p><span class="label">Categoría:</span> <span id="catProactiva">Redes</span></p>
      <p><span class="label">Eviden

