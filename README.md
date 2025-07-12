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
body {
  margin: 0;
  font-family: 'Arial', sans-serif;
  background-image: url('images/fondo-jungla.jpg');
  background-size: cover;
  background-position: center;
  color: white;
  text-align: center;
}

.container {
  padding-top: 60px;
}

.logo {
  width: 300px;
}

.contador, .pregunta, .nivel, .tiempo {
  font-size: 24px;
}

input {
  font-size: 20px;
  padding: 5px;
  margin: 10px;
  width: 150px;
}

button {
  padding: 10px 20px;
  font-size: 18px;
  cursor: pointer;
}

.ranking {
  margin-top: 20px;
}
let puntos = 0;
let num1, num2;
let tiempo = 60;
let nivel = 1;
let ranking = [];

function nuevaPregunta() {
  num1 = Math.floor(Math.random() * 100) + 1;
  num2 = Math.floor(Math.random() * 100) + 1;
  document.getElementById('pregunta').innerText = `¿Cuánto es ${num1} + ${num2}?`;
}

function verificar() {
  const respuesta = parseInt(document.getElementById('respuesta').value);
  if (respuesta === num1 + num2) {
    puntos++;
  } else {
    puntos = 0;
  }
  document.getElementById('contador').innerText = `Puntos: ${puntos}`;
  nuevaPregunta();
  if (puntos > 10 && nivel === 1) {
    nivel = 2;
    document.getElementById('nivel').innerText = 'Nivel 2: ¡Contrarreloj!';
    tiempo = 60;
    startTimer();
  }
}

function reiniciar() {
  puntos = 0;
  nivel = 1;
  document.getElementById('nivel').innerText = 'Nivel 1';
  document.getElementById('contador').innerText = 'Puntos: 0';
  document.getElementById('tiempo').innerText = 'Tiempo restante: 60';
  nuevaPregunta();
}

function startTimer() {
  let timer = setInterval(function() {
    if (tiempo <= 0) {
      clearInterval(timer);
      alert("¡Se acabó el tiempo! Puntuación final: " + puntos);
      ranking.push(puntos);
      ranking.sort((a, b) => b - a);
      updateRanking();
    } else {
      document.getElementById('tiempo').innerText = 'Tiempo restante: ' + tiempo;
      tiempo--;
    }
  }, 1000);
}

function updateRanking() {
  const rankingList = document.getElementById('ranking-list');
  rankingList.innerHTML = '';
  ranking.slice(0, 5).forEach((score, index) => {
    const li = document.createElement('li');
    li.textContent = `#${index + 1}: ${score} puntos`;
    rankingList.appendChild(li);
  });
}

window.onload = nuevaPregunta;
