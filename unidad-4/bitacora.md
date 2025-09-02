# Evidencias de la unidad 4

## Explicación conceptual de la obra

* ¿Qué concepto de la unidad 4 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Sistemas de partículas. La obra representa un sistema compuesto por múltiples péndulos que actúan como elementos individuales dentro de un conjunto que genera un comportamiento complejo y visualmente armónico.

* ¿Qué concepto de la unidad 3 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Oscilaciones. Cada péndulo sigue un movimiento oscilatorio basado en la física del péndulo simple, aplicando aceleración angular, velocidad angular y amortiguamiento.

* ¿Qué concepto de la unidad 2 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Fuerzas aplicadas externamente. Se simula el viento aplicando una fuerza angular hacia la izquierda o derecha cuando se presionan las teclas "A" o "D".

* ¿Qué concepto de la unidad 1 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Velocidad constante y amortiguamiento. Los péndulos oscilan con velocidad angular que se modifica por aceleración y se reduce con amortiguamiento (damping), creando un movimiento natural.

## ¿Cómo resolviste la interacción?
> Tu respuesta aquí:
> Color aleatorio y vectores. Se usa p5.Vector para calcular posiciones del péndulo, y el color global de todos los péndulos cambia aleatoriamente cada 2 segundos

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra](https://editor.p5js.org/DaviSlime/full/8H5HM04wL)

## Código de la obra 

``` js
let pendulums = [];
let numPendulums = 20;
let globalColor;
let gravity = 0.4;

let windForce = 0;
let lastColorChangeTime = 0;
let colorChangeInterval = 2000; // 2 segundos

function setup() {
  createCanvas(800, 600);
  globalColor = randomColor();

  let pivotX = width / 2;
  let pivotY = 100;

  for (let i = 0; i < numPendulums; i++) {
    let r = random(80, 300);
    pendulums.push(new Pendulum(pivotX, pivotY, r));
  }
}

function draw() {
  background(240);

  // Cambiar color cada 2 segundos
  if (millis() - lastColorChangeTime > colorChangeInterval) {
    globalColor = randomColor();
    lastColorChangeTime = millis();
  }

  for (let p of pendulums) {
    p.applyWind(windForce);
    p.update();
    p.drag();
    p.display();
  }
}

// Función auxiliar para generar color aleatorio
function randomColor() {
  return color(random(255), random(255), random(255));
}

// Mouse Interacción
function mousePressed() {
  for (let p of pendulums) {
    p.clicked(mouseX, mouseY);
  }
}

function mouseReleased() {
  for (let p of pendulums) {
    p.stopDragging();
  }
}

// Teclado para simular viento
function keyPressed() {
  if (key === 'a' || key === 'A') {
    windForce = -0.001;
  } else if (key === 'd' || key === 'D') {
    windForce = 0.001;
  }
}

function keyReleased() {
  if (key === 'a' || key === 'A' || key === 'd' || key === 'D') {
    windForce = 0;
  }
}

// Clase Pendulum
class Pendulum {
  constructor(x, y, r) {
    this.pivot = createVector(x, y);
    this.r = r;
    this.angle = PI / 4;
    this.angleVelocity = 0;
    this.angleAcceleration = 0;
    this.damping = 0.995;
    this.ballr = 10;
    this.dragging = false;
    this.bob = createVector();
  }

  applyWind(force) {
    if (!this.dragging) {
      this.angleAcceleration += force;
    }
  }

  update() {
    if (!this.dragging) {
      this.angleAcceleration += (-1 * gravity / this.r) * sin(this.angle);
      this.angleVelocity += this.angleAcceleration;
      this.angle += this.angleVelocity;
      this.angleVelocity *= this.damping;
      this.angleAcceleration = 0;
    }
  }

  display() {
    this.bob.set(this.r * sin(this.angle), this.r * cos(this.angle));
    this.bob.add(this.pivot);

    stroke(0);
    strokeWeight(2);
    line(this.pivot.x, this.pivot.y, this.bob.x, this.bob.y);

    fill(globalColor);
    stroke(0);
    strokeWeight(1);
    ellipse(this.bob.x, this.bob.y, this.ballr * 2);
  }

  clicked(mx, my) {
    let d = dist(mx, my, this.bob.x, this.bob.y);
    if (d < this.ballr) {
      this.dragging = true;
    }
  }

  stopDragging() {
    this.angleVelocity = 0;
    this.dragging = false;
  }

  drag() {
    if (this.dragging) {
      let diff = p5.Vector.sub(this.pivot, createVector(mouseX, mouseY));
      this.angle = atan2(-diff.y, diff.x) - HALF_PI;
    }
  }
}

```

## Captura de pantalla representativa


<img width="810" height="604" alt="image" src="https://github.com/user-attachments/assets/3d26e071-473c-47f6-a948-ddfd5946b453" />





