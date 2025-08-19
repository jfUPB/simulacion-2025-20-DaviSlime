
# Unidad 2


## 🛠 Fase: Apply

No está la actividad. Esta nota la deja el profesor.


1. Concepto de la obra generativa:
La obra representa un enjambre de partículas que reaccionan al cursor, alternando entre atracción, repulsión y movimiento aleatorio, creando un sistema visual dinámico y cambiante.

2. Aplicación del marco MOTION 101:
Lo aplico definiendo fuerzas (atracción, repulsión, ruido) que afectan la aceleración; estas se traducen en velocidad y posición, generando movimiento emergente coherente.

3. Algoritmo de aceleración:
Uso la ley inversa cuadrática de la gravedad porque permite simular comportamientos realistas y orgánicos en la interacción con el mouse.

4. Interactividad en tiempo real:
El mouse define el punto de atracción/repulsión, el teclado cambia el comportamiento (a, s, d), y la barra espaciadora controla las estelas, permitiendo al usuario influir directamente en la estética generada.

| Tecla           | Función                                        |
| --------------- | ---------------------------------------------- |
| **Espacio ( )** | Activa o desactiva la estela (trail).          |
| **R**           | Reinicia las partículas.                       |
| **A**           | Cambia a modo *repel* (repulsión).             |
| **S**           | Cambia a modo *random* (movimiento aleatorio). |
| **D**           | Cambia a modo *attract* (atracción).           |


6. El código de la aplicación.
```javascript
let particles = [];
let G = 100; 
let trail = true;
let behavior = "attract";

function setup() {
  createCanvas(800, 600);
  colorMode(HSB, 360, 100, 100, 100);
  for (let i = 0; i < 150; i++) {
    particles.push(new Particle());
  }
  background(0);
}

function draw() {
  if (!trail) {
    background(0, 10);
  }

  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];

    if (behavior === 'attract') {
      p.attracted(createVector(mouseX, mouseY));
    } else if (behavior === 'repel') {
      p.repelled(createVector(mouseX, mouseY));
    } else if (behavior === 'random') {
      p.randomMotion();
    }

    p.update();
    p.show();


    if (p.alpha <= 0) {
      particles.splice(i, 1);

      particles.push(new Particle());
    }
  }
}

function keyPressed() {
  if (key === ' ') {
    trail = !trail;
  }
  if (key === 'r' || key === 'R') {
    particles = [];
    for (let i = 0; i < 150; i++) {
      particles.push(new Particle());
    }
    background(0);
  }
  if (key === 'a' || key === 'A') {
    behavior = 'repel';
  }
  if (key === 's' || key === 'S') {
    behavior = 'random';
  }
  if (key === 'd' || key === 'D') {
    behavior = 'attract';
  }
}

class Particle {
  constructor() {

    let x = randomGaussian(width / 2, width / 6);
    let y = randomGaussian(height / 2, height / 6);
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(0.5, 2));
    this.acc = createVector();
    this.r = random(2, 5);
    this.maxSpeed = 6;

    this.hue = random(360);
    this.alpha = 100; // Opacidad inicial
    this.fadeRate = random(0.1, 0.5); // Desvanecimiento por frame
  }

  attracted(target) {
    let force = p5.Vector.sub(target, this.pos);
    let d = constrain(force.mag(), 5, 100);
    force.normalize();
    let strength = G / (d * d);
    force.mult(strength * 3); 
    this.acc = force;
  }

  repelled(target) {
    let force = p5.Vector.sub(this.pos, target); 
    let d = constrain(force.mag(), 5, 100);
    force.normalize();
    let strength = G / (d * d);
    force.mult(strength * 3); 
    this.acc = force;
  }

  randomMotion() {
    let angle = noise(this.pos.x * 0.01, this.pos.y * 0.01, frameCount * 0.01) * TWO_PI * 4;
    let force = p5.Vector.fromAngle(angle);
    force.mult(0.2);
    this.acc = force;
  }

  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0); 
    this.alpha -= this.fadeRate;
    this.alpha = max(0, this.alpha);
  }

  show() {
    noStroke();
    fill(this.hue, 80, 100, this.alpha);
    ellipse(this.pos.x, this.pos.y, this.r * 2);
  }
}

```

7. Un enlace al proyecto en el editor de p5.js.
https://editor.p5js.org/DaviSlime/sketches/piTN3nkl5

8. Una captura de pantalla representativa de tu pieza de arte generativo.
<img width="919" height="747" alt="image" src="https://github.com/user-attachments/assets/8dfd7982-ecc0-4ee0-a971-1657b7872b27" />

