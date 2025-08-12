# Unidad 3

## 🔎 Fase: Set + Seek


## Actividad 9

Inventa tres obras generativas interactivas, uno para cada una de las siguientes fuerzas:

* Fricción.
* Resistencia del aire y de fluidos.
* Atracción gravitacional.

1. Explica cómo modelaste cada fuerza.
2. Conceptualmente cómo se relaciona la fuerza con la obra generativa.
3. Copia el enlace a tu ejemplo en p5.js.
4. Copia el código.
5. Captura una imagen representativa de tu ejemplo.


usa todas estas actividades para hacer una obra de arte generativo que aplica la fuerza de friccion donde con las flechas cambie la direccion de la gravedad, y cada lado de la pantalla tenga una friccion diferente ten en cuenta que el codigo se debe hacer con base en la sección Modeling forces del texto nature of code

CODIGO PROVISIONAL

```javascript
let mover;
let gravity;
let leftFriction = 0.1;
let rightFriction = 0.01;

function setup() {
  createCanvas(800, 400);
  mover = new Mover();
  gravity = createVector(0, 0.1); // Gravedad inicial hacia abajo
}

function draw() {
  background(240);

  // Aplicar gravedad
  let weight = p5.Vector.mult(gravity, mover.mass);
  mover.applyForce(weight);

  // Aplicar fricción (dependiendo del lado en que esté el objeto)
  let friction = mover.velocity.copy();
  friction.normalize();
  friction.mult(-1);

  if (mover.position.x < width / 2) {
    friction.mult(leftFriction);
  } else {
    friction.mult(rightFriction);
  }

  mover.applyForce(friction);

  // Actualizar y dibujar
  mover.update();
  mover.checkEdges();
  mover.show();
}

// Cambiar la dirección de la gravedad con flechas
function keyPressed() {
  if (keyCode === UP_ARROW) {
    gravity = createVector(0, -0.1);
  } else if (keyCode === DOWN_ARROW) {
    gravity = createVector(0, 0.1);
  } else if (keyCode === LEFT_ARROW) {
    gravity = createVector(-0.1, 0);
  } else if (keyCode === RIGHT_ARROW) {
    gravity = createVector(0.1, 0);
  }
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector();
    this.acceleration = createVector();
    this.mass = 2;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass); // a = F / m
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); // Resetear aceleración al final del frame
  }

  checkEdges() {
    if (this.position.x > width) {
      this.position.x = width;
      this.velocity.x *= -1;
    } else if (this.position.x < 0) {
      this.position.x = 0;
      this.velocity.x *= -1;
    }

    if (this.position.y > height) {
      this.position.y = height;
      this.velocity.y *= -1;
    } else if (this.position.y < 0) {
      this.position.y = 0;
      this.velocity.y *= -1;
    }
  }

  show() {
    stroke(0);
    fill(127);
    ellipse(this.position.x, this.position.y, this.mass * 16);
  }
}

```
