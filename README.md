# Isla-Magica
Juego matematico
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Isla Matemática</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <img src="images/logo-isla-matematica.png" alt="Isla Matemática" class="logo">
    <div id="contador" class="contador">Puntos: 0</div>
    <div id="pregunta" class="pregunta"></div>
    <input type="number" id="respuesta" placeholder="Tu respuesta">
    <button onclick="verificar()">Responder</button>
    <button onclick="reiniciar()">Reiniciar Juego</button>
    <div id="nivel" class="nivel">Nivel 1</div>
    <div id="tiempo" class="tiempo">Tiempo restante: 60</div>
    <div id="ranking" class="ranking">
      <h3>Ranking</h3>
      <ul id="ranking-list"></ul>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>
