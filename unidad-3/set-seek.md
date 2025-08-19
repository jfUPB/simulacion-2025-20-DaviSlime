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

#### FRICCIÓN

1. ¿Cómo se modeló la fuerza de fricción?

La fricción se modela como una fuerza que siempre se opone al movimiento del objeto. Se calcula tomando la velocidad, normalizándola para obtener solo la dirección, y multiplicándola por un coeficiente de fricción específico según la zona en la que se encuentre el objeto. Esta fuerza se aplica en dirección contraria a la velocidad para desacelerar el objeto.

2. Relación conceptual con la obra generativa

La fuerza de fricción afecta el movimiento del objeto y, por tanto, el patrón visual que deja al moverse. Al variar la fricción según la zona, el sistema genera trayectorias y estelas diferentes, creando una interacción dinámica entre las reglas físicas y la expresión visual de la obra generativa.

3. https://editor.p5js.org/DaviSlime/sketches/nzunBqA6K

4. CODIGO

```javascript
let mover;
let gravity;
let frictionZones = [];

function setup() {
  createCanvas(800, 400);
  mover = new Mover();
  gravity = createVector(0, 0.1); // Gravedad inicial hacia abajo

  // Crear zonas con diferentes fricciones (horizontal)
  let zoneWidth = width / 4;
  frictionZones = [
    { x: 0, w: zoneWidth, friction: 0.2, color: color(255, 0, 0) },       // Rojo - alta fricción
    { x: zoneWidth, w: zoneWidth, friction: 0.1, color: color(255, 255, 0) }, // Amarillo - media
    { x: zoneWidth * 2, w: zoneWidth, friction: 0.05, color: color(0, 255, 0) }, // Verde - baja
    { x: zoneWidth * 3, w: zoneWidth, friction: 0.15, color: color(255, 150, 0) } // Naranja - media-alta
  ];

  // Dibujar fondo fijo de zonas de fricción (solo una vez)
  noStroke();
  for (let zone of frictionZones) {
    fill(zone.color);
    rect(zone.x, 0, zone.w, height);
  }
}

function draw() {
  // Pintar fondo con transparencia (para rastro)
  fill(240, 240, 240, 20);
  rect(0, 0, width, height);

  // Aplicar gravedad
  let weight = p5.Vector.mult(gravity, mover.mass);
  mover.applyForce(weight);

  // Calcular fricción según la zona
  for (let zone of frictionZones) {
    if (mover.position.x > zone.x && mover.position.x < zone.x + zone.w) {
      let friction = mover.velocity.copy();
      friction.normalize();
      friction.mult(-1);
      friction.mult(zone.friction);
      mover.applyForce(friction);
      break;
    }
  }

  mover.update();
  mover.checkEdges();
  mover.show();
}

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
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
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
    fill(50, 100); // Bolita más opaca para que el rastro se note
    ellipse(this.position.x, this.position.y, this.mass * 16);
  }
}

```

5. <img width="793" height="399" alt="image" src="https://github.com/user-attachments/assets/cb7482e4-e03e-4ca0-a376-9cba83f6b005" />



#### Resistencia del aire y de fluidos



1. Modelado de fuerzas:
La fuerza constante impulsa la bolita horizontalmente (izquierda o derecha). La resistencia del fluido se modela como una fuerza de fricción que va en sentido opuesto a la velocidad, proporcional al cuadrado de la velocidad y al coeficiente de resistencia según el medio (agua, miel, viento o vacío).

2. Relación con la obra generativa:
Las fuerzas físicas generan movimientos dinámicos que producen patrones visuales cambiantes. Al modificar la resistencia y la dirección, el sistema crea una interacción visual que refleja las reglas físicas, convirtiendo las fuerzas en elementos artísticos dentro de la obra generativa.

3. https://editor.p5js.org/DaviSlime/sketches/J101SvAKM

4. Código

```javascript
let mover;
let resistanceType = 'none'; // tipo de resistencia actual
let resistanceCoefficients = {
  none: 0,
  wind: 0.01,
  water: 0.1,
  honey: 0.3
};
let direction = 1; // 1 para derecha, -1 para izquierda

function setup() {
  createCanvas(800, 400);
  mover = new Mover();
  createP('Presiona las flechas para cambiar de izquierda a derecha y la tecla A para cambiar a el agua, V para el viento, M para la miel y Space para resistencia 0');
}

function draw() {
  // Cambiar fondo según resistencia
  if (resistanceType === 'water') {
    background(0, 100, 255); // azul agua
  } else if (resistanceType === 'honey') {
    background(180, 140, 70); // color miel
  } else if (resistanceType === 'wind') {
    background(200, 230, 255); // azul claro viento
  } else {
    background(240); // sin resistencia, fondo gris claro
  }

  // Fuerza constante para mover la bolita en la dirección indicada
  let windForce = createVector(0.1 * direction, 0);
  mover.applyForce(windForce);

  // Aplicar resistencia según tipo
  let c = resistanceCoefficients[resistanceType];
  if (c > 0) {
    let speed = mover.velocity.mag();
    if (speed > 0) {
      let dragMagnitude = c * speed * speed;
      let drag = mover.velocity.copy();
      drag.mult(-1);
      drag.normalize();
      drag.mult(dragMagnitude);
      mover.applyForce(drag);
    }
  }

  mover.update();
  mover.checkEdges();
  mover.show();
}

function keyPressed() {
  if (key === 'a' || key === 'A') {
    resistanceType = 'water';
  } else if (key === 'm' || key === 'M') {
    resistanceType = 'honey';
  } else if (key === 'v' || key === 'V') {
    resistanceType = 'wind';
  } else if (key === ' ') {
    resistanceType = 'none';
  }

  if (keyCode === LEFT_ARROW) {
    direction = -1;
  } else if (keyCode === RIGHT_ARROW) {
    direction = 1;
  }
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
    this.mass = 1;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  checkEdges() {
    // Rebote en los bordes horizontales
    if (this.position.x > width) {
      this.position.x = width;
      this.velocity.x *= -1;
    }
    if (this.position.x < 0) {
      this.position.x = 0;
      this.velocity.x *= -1;
    }
  }

  show() {
    fill(127);
    stroke(0);
    ellipse(this.position.x, this.position.y, 32, 32);
  }
}

```

5.
Resistencia 0: 

<img width="888" height="468" alt="image" src="https://github.com/user-attachments/assets/91668758-7b2b-4e73-a48d-e9d785744b17" />


Resistencia del agua: 
<img width="887" height="471" alt="image" src="https://github.com/user-attachments/assets/9b872038-03e0-446e-8580-ce91adb9cd4c" />


Resistencia del viento: 
<img width="889" height="470" alt="image" src="https://github.com/user-attachments/assets/192af742-3bce-48ed-a9db-b150ffaab7d5" />


Resistencia de la miel: 
<img width="887" height="440" alt="image" src="https://github.com/user-attachments/assets/d63e03db-b903-4f1d-9b63-4ba80b369d05" />



#### Atracción gravitacional

1. Modelado de fuerzas:
Se usó la ley de gravitación universal, calculando la atracción según masa y distancia, y aplicándola como aceleración a cada partícula.

2. Relación con la obra generativa:
La fuerza guía el movimiento de las partículas, creando patrones dinámicos y orgánicos que simulan un sistema vivo alrededor del agujero negro.

4. [https://editor.p5js.org/DaviSlime/sketches/J101SvAKM](https://editor.p5js.org/DaviSlime/sketches/nWLL9cHTj)

5. Código

```javascript
let movers = [];
let blackHole;
let G = 1;

function setup() {
  createCanvas(1200, 800);
  blackHole = new Attractor(width / 2, height / 2, 20);

  // Crear partículas (sin velocidad inicial)
  for (let i = 0; i < 300; i++) {
    let m = new Mover(random(width), random(height), random(0.5, 2));
    movers.push(m);
  }

  background(0);
}

function draw() {
  fill(0, 25);
  noStroke();
  rect(0, 0, width, height);

  blackHole.show();

  for (let i = movers.length - 1; i >= 0; i--) {
    let mover = movers[i];

    // Aplicar atracción gravitacional
    let force = blackHole.attract(mover);
    mover.applyForce(force);

    mover.update();
    mover.show();

    // Si está muy cerca del agujero negro, eliminar
    let d = p5.Vector.dist(mover.position, blackHole.position);
    if (d < blackHole.radius) {
      movers.splice(i, 1);
    }
  }

  // Mantener cantidad de partículas constante
  while (movers.length < 300) {
    let m = new Mover(random(width), random(height), random(0.5, 2));
    movers.push(m);
  }
}

function keyPressed() {
  if (key === ' ') {
    G = 3;
  }
}

function keyReleased() {
  if (key === ' ') {
    G = 1;
  }
}

class Mover {
  constructor(x, y, mass) {
    this.mass = mass;
    this.radius = mass * 4;
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0); // Sin velocidad inicial
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    stroke(255, 200);
    strokeWeight(2);
    point(this.position.x, this.position.y);
  }
}

class Attractor {
  constructor(x, y, mass) {
    this.mass = mass;
    this.radius = mass * 2;
    this.position = createVector(x, y);
  }

  attract(m) {
    let force = p5.Vector.sub(this.position, m.position);
    let distanceSq = constrain(force.magSq(), 100, 10000);
    let strength = (G * this.mass * m.mass) / distanceSq;
    force.setMag(strength);
    return force;
  }

  show() {
    // Halo
    for (let r = this.radius * 3; r > this.radius; r -= 1) {
      fill(255, map(r, this.radius, this.radius * 3, 10, 0));
      noStroke();
      ellipse(this.position.x, this.position.y, r * 2);
    }

    // Centro negro
    fill(0);
    stroke(255);
    strokeWeight(1);
    ellipse(this.position.x, this.position.y, this.radius * 2);
  }
}

```


