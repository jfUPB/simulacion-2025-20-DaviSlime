# Unidad 1

## 🛠 Fase: Apply

### Actividad 8

Vas a crear una obra generativa interactiva en tiempo real utilizando los conceptos de aleatoriedad que has aprendido en esta unidad.
Tu obra debe:

- Usar al menos tres conceptos estudiados en esta unidad COMBINADOS de manera creativa y coherente.
- Tu obra de ser interactiva y generativa en tiempo real. Puedes usar el mouse, el teclado o cualquier otro sensor de entrada para interactuar con la obra.

El concepto de la obra generativa es un minijuego donde debes pasar de un lado a otro pasando por las barreras de colores sin tocarlas tambien si la bolita cambia de color a azul te da una inmunidad tienes 3 vidas.

#### Codigo

```javascript
let player;
let numBarriers = 10;
let noiseOffsets = [];
let lastDeactivation = [];
let deactivated = [];
let barrierColors = [];

let immunity = false;
let immunityStart = 0;
let flashBackground = false;
let flashTimer = 0;
let time = 0;

let lives = 3;
let gameOver = false;

function setup() {
  createCanvas(1200, 800);
  player = createVector(width/2, height/2);

  for (let i = 0; i < numBarriers; i++) {
    noiseOffsets[i] = random(1000);
    lastDeactivation[i] = 0;
    deactivated[i] = false;
    barrierColors[i] = color(random(100, 255), random(100, 255), random(100, 255));
  }
}

function draw() {
  if (gameOver) {
    drawGameOverScreen();
    return; // No actualizar más mientras perdimos
  }

  if (flashBackground && millis() - flashTimer < 200) {
    background(255, 0, 0);
  } else {
    background(30);
    flashBackground = false;
  }

  // Control jugador
  player.x = mouseX;
  player.y = mouseY;

  // Dibujar jugador
  noStroke();
  fill(immunity ? color(0, 255, 255) : color(255));
  ellipse(player.x, player.y, 20);

  // Dibujar barreras
  for (let i = 0; i < numBarriers; i++) {
    let baseY = map(i, 0, numBarriers - 1, 50, height - 50);
    let xStep = 5;

    if (frameCount % 60 === 0 && !deactivated[i]) {
      let randVal = random(100);
      if (randVal < 10) {
        deactivated[i] = true;
        lastDeactivation[i] = millis();
      }
    }

    if (deactivated[i] && millis() - lastDeactivation[i] > 2000) {
      deactivated[i] = false;
    }

    if (!deactivated[i]) {
      stroke(barrierColors[i]);
      strokeWeight(2);
      noFill();

      beginShape();
      for (let x = 0; x <= width; x += xStep) {
        let noiseVal = noise(x * 0.005, time + noiseOffsets[i]);
        let offsetY = map(noiseVal, 0, 1, -20, 20);
        let y = baseY + offsetY;
        vertex(x, y);

        if (!immunity && dist(player.x, player.y, x, y) < 10) {
          hitBarrier();
        }
      }
      endShape();
    }
  }

  // Activar inmunidad aleatoria
  if (frameCount % 120 === 0 && !immunity) {
    let chance = random(100);
    if (chance < 3) {
      immunity = true;
      immunityStart = millis();
    }
  }

  if (immunity && millis() - immunityStart > 5000) {
    immunity = false;
  }

  time += 0.01;

  // Mostrar vidas en pantalla
  fill(255);
  textSize(24);
  text("Vidas: " + lives, 20, 30);
}

function hitBarrier() {
  // Evitar múltiples restas rápidas
  if (flashBackground) return;

  lives--;
  flashBackground = true;
  flashTimer = millis();

  if (lives <= 0) {
    gameOver = true;
  }
}

function drawGameOverScreen() {
  background(0, 150);
  fill(255);
  textAlign(CENTER, CENTER);
  textSize(48);
  text("¡Perdiste!", width/2, height/2 - 50);
  textSize(24);
  text("Haz clic para reiniciar", width/2, height/2 + 20);
}

function mousePressed() {
  if (gameOver) {
    restartGame();
  }
}

function restartGame() {
  lives = 3;
  gameOver = false;
  immunity = false;
  flashBackground = false;
  time = 0;
  player.set(width/2, height/2);

  for (let i = 0; i < numBarriers; i++) {
    noiseOffsets[i] = random(1000);
    lastDeactivation[i] = 0;
    deactivated[i] = false;
  }
}

```

*Enlace a la experiencia:* https://editor.p5js.org/DaviSlime/full/g9QMjRZaS



https://github.com/user-attachments/assets/92ce5e7d-0225-4fa3-a6ba-5d3974f7011b

