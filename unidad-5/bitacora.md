# Evidencias de la unidad 5

## Actividad 2


### 1- El ejemplo 4.2: an Array of Particles.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

**Creación:**
Se crean nuevas instancias de ``Particle`` en cada frame con ``addParticle()`` y se agregan a un ``ArrayList<Particle>``.

**Desaparición:**
Cada partícula tiene una propiedad ``lifespan`` que decrece con el tiempo.
Cuando el `lifespan`` llega a 0, se considera "muerta".

**Gestión de memoria:**
En el método ``run()``, se hace un loop por el ArrayList y se eliminan las partículas muertas con ``particles.remove(i)``.
Esto evita que se acumulen en memoria.

----

### 2- El ejemplo 4.4: a System of Systems.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

**Creación:**
Se crean múltiples sistemas de partículas ``(ParticleSystem)`` en posiciones aleatorias.
Cada sistema gestiona su propio ``ArrayList<Particle>``.

**Desaparición:**
Igual que antes: cada partícula tiene un ``lifespan`` y se elimina cuando muere.
El sistema también puede eliminar partículas muertas de su lista.

**Gestión de memoria:**
Cada sistema limpia su propio ``array`` eliminando las partículas muertas.
Los sistemas pueden mantenerse activos indefinidamente, pero sus partículas se reciclan correctamente.

----

### 3- El ejemplo 4.5: a Particle System with Inheritance and Polymorphism.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

**Creación:**
En cada frame, se crean nuevas instancias de distintas subclases de Particle (por ejemplo, Confetti) utilizando herencia y polimorfismo, a través del método addParticle(). Estas instancias se agregan a un ``ArrayList<Particle>``.

**Desaparición:**
Cada partícula tiene una propiedad ``lifespan`` que decrece con el tiempo. Cuando ``lifespan`` llega a 0, se considera que la partícula está "muerta".

**Gestión de memoria:**
Durante el método ``run()``, se recorre el ``ArrayList`` y se eliminan las partículas muertas utilizando ``particles.remove(i)``. Esto asegura que no se acumulen objetos innecesarios en memoria, incluso si provienen de diferentes clases gracias al uso del polimorfismo.

----

### 4- El ejemplo 4.6: a Particle System with Forces.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

**Creación:**
Se generan nuevas partículas en cada frame con ``addParticle()`` y se agregan a un ``ArrayList<Particle>``. Las partículas pueden ser instancias de diferentes tipos gracias al uso de clases derivadas.

**Desaparición:**
Cada partícula tiene un ``lifespan`` que disminuye progresivamente. Cuando este valor llega a cero o menos, la partícula se considera "muerta".

**Gestión de memoria:**
Las partículas se recorren con un loop en el método ``run()`` del sistema. Las que están muertas se eliminan de la lista con ``particles.remove(i)``, liberando así memoria. Además, se aplican fuerzas externas como la gravedad o el viento que afectan la física pero no interfieren directamente con la gestión de memoria.

----

### 5- El ejemplo 4.7: a Particle System with a Repeller.

 
 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

**Creación:**
Se siguen creando partículas nuevas cada frame con ``addParticle()`` y se agregan a un ``ArrayList<Particle>`` como en los ejemplos anteriores.

**Desaparición:**
Cada partícula posee un ``lifespan`` que decrece a lo largo del tiempo. Una vez que este valor llega a 0, la partícula se considera "muerta".

**Gestión de memoria:**
El método ``run()`` itera sobre el ``ArrayList`` y elimina las partículas muertas con ``particles.remove(i)``, previniendo acumulaciones en memoria. Aunque en este caso se introduce un objeto adicional (Repeller) que aplica una fuerza de repulsión a las partículas, esto no afecta directamente la gestión de memoria, que sigue manejándose de forma eficiente mediante la eliminación de objetos no utilizados.

----

## Modificacion de codigos de Ejemplo

### ejemplo 4.2: an Array of Particles:

En cada cuadro (draw()), hice que se creara una nueva partícula con particles.push(new Particle(...)). Esto simula un flujo constante de partículas, como si se estuvieran generando del emitter, ademas se recorre el arreglo particles de atrás hacia adelante para evitar errores al eliminar elementos, Se verifica con isDead() si la partícula ya ha "muerto" (cuando su lifespan es menor que 0).

Si está muerta, se elimina del arreglo con splice(i, 1), liberando memoria.


Aplicación: Cada partícula tiene una propiedad lifespan que disminuye con el tiempo (this.lifespan -= 2). Este enfoque simula el envejecimiento de las partículas y permite removerlas del arreglo una vez que han cumplido su ciclo de vida, lo cual libera memoria y evita acumulación innecesaria de objetos, mejorando el rendimiento de la simulación.

### Enlace al codigo
https://editor.p5js.org/DaviSlime/full/C--32xkZQ


### Codigo del proyecto:

```js
let particles = [];
let currentColor;

function setup() {
  createCanvas(640, 240);
  currentColor = color(0); // Color inicial
}

function draw() {
  background(255);
  
  // Agregamos nueva partícula en cada frame
  particles.push(new Particle(width / 2, 20, currentColor));
  
  // Recorrer en reversa para eliminar partículas muertas
  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    if (particle.isDead()) {
      particles.splice(i, 1);
    }
  }
}

function keyPressed() {
  if (key === ' ') {
    // Cambiar a un color aleatorio
    currentColor = color(random(255), random(255), random(255));
  }
}

// Clase Particle
class Particle {
  constructor(x, y, col) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-2, 0));
    this.acceleration = createVector(0, 0.05);
    this.lifespan = 255;
    this.color = col;
  }

  run() {
    this.update();
    this.display();
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
  }

  display() {
    noStroke();
    fill(red(this.color), green(this.color), blue(this.color), this.lifespan);
    ellipse(this.position.x, this.position.y, 12);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

```

### Captura de pantalla

<img width="715" height="329" alt="image" src="https://github.com/user-attachments/assets/d22b6fba-6f68-43e6-a0f9-5c195d42529a" />


### Ejemplo 4.4: a System of Systems.


### 1. Creación y eliminación de partículas
- Cada **click** genera una nueva constelación de partículas en el punto del mouse.  
- Todas las constelaciones se acumulan en memoria dentro de un arreglo (`constellations`).  
- Al presionar la **barra espaciadora**, el arreglo se vacía (`constellations = []`), eliminando todas las partículas.  
- El **garbage collector** de JavaScript se encarga de limpiar la memoria de las partículas eliminadas.

### 2. Conceptos aplicados
- **Motion 101:** cada partícula tiene posición, velocidad y aceleración. Esto da un movimiento fluido y natural.  
- **Sistemas de partículas (Example 4.2):** varias partículas se agrupan en constelaciones y se conectan con líneas cuando están cerca.  

### 3. Enlace al editor

https://editor.p5js.org/DaviSlime/sketches/hNmkPinUl

### 4. Codigo fuente

```js
let constellations = []; // Array de constelaciones (cada una con varias partículas)

function setup() {
  createCanvas(800, 600);
}

function draw() {
  drawBackground();

  let allParticles = [];

  // Dibujar partículas y recolectarlas en un solo arreglo
  for (let constellation of constellations) {
    for (let p of constellation) {
      p.update();
      p.edges();
      p.show();
      allParticles.push(p);
    }
  }

  // Conectar TODAS las partículas entre sí
  for (let i = 0; i < allParticles.length; i++) {
    for (let j = i + 1; j < allParticles.length; j++) {
      let d = dist(
        allParticles[i].pos.x, allParticles[i].pos.y,
        allParticles[j].pos.x, allParticles[j].pos.y
      );
      if (d < 100) { // rango de conexión
        stroke(255, 180);
        strokeWeight(0.5);
        line(
          allParticles[i].pos.x, allParticles[i].pos.y,
          allParticles[j].pos.x, allParticles[j].pos.y
        );
      }
    }
  }
}

// Fondo tipo cielo nocturno con degradado
function drawBackground() {
  for (let y = 0; y < height; y++) {
    let inter = map(y, 0, height, 0, 1);
    let c = lerpColor(color(10, 10, 30), color(0, 0, 10), inter);
    stroke(c);
    line(0, y, width, y);
  }
}

// Crear nueva constelación en el punto del click
function mousePressed() {
  let newConstellation = [];
  let numParticles = int(random(8, 15)); // cantidad de estrellas en la constelación

  for (let i = 0; i < numParticles; i++) {
    let p = new Particle(mouseX + random(-50, 50), mouseY + random(-50, 50));
    newConstellation.push(p);
  }
  constellations.push(newConstellation);
}

// Borrar todas las constelaciones con la barra espaciadora
function keyPressed() {
  if (key === ' ') {
    constellations = [];
  }
}

// Clase Particle usando Motion 101 con parpadeo
class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(0.1, 0.5)); // velocidad más lenta
    this.acc = createVector(0, 0);
    this.r = random(2, 4);
    this.offset = random(1000); // desfase para el parpadeo
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  applyForce(force) {
    this.acc.add(force);
  }

  edges() {
    // Rebote en los bordes
    if (this.pos.x < 0 || this.pos.x > width) this.vel.x *= -1;
    if (this.pos.y < 0 || this.pos.y > height) this.vel.y *= -1;
  }

  show() {
    noStroke();
    // Parpadeo suave con sinusoide
    let flicker = map(sin(frameCount * 0.05 + this.offset), -1, 1, 180, 255);
    let size = this.r + map(sin(frameCount * 0.05 + this.offset), -1, 1, -0.5, 1.5);

    fill(255, 255, 200, flicker);
    ellipse(this.pos.x, this.pos.y, size * 2);
  }
}

```
### Captura de pantalla

<img width="920" height="730" alt="image" src="https://github.com/user-attachments/assets/65502e47-feb4-4a20-a341-24289aa34191" />


## Ejemplo 4.5: a Particle System with Inheritance and Polymorphism.

### 1. Gestión de creación, desaparición de partículas y memoria

La creación de partículas se maneja añadiendo nuevos objetos al array `pinceles` tanto al iniciar la simulación en `setup()` como al hacer clic con el mouse (`mousePressed()`). Cada clic agrega un conjunto de partículas nuevas en la posición del cursor.

En cuanto a la desaparición, el código **no implementa ningún mecanismo para eliminar partículas**. Esto significa que una vez creadas, las partículas permanecen activas y se actualizan continuamente. Como resultado, la memoria utilizada por la simulación crece conforme se agregan más partículas y no se liberan recursos.


### 2. Concepto aplicado, cómo y por qué

El concepto aplicado es el de un **sistema dinámico de partículas**, donde las partículas son creadas, actualizadas y renderizadas continuamente. Se aplica la creación dinámica en respuesta a eventos (clics) para enriquecer la composición visual.

Sin embargo, no se implementa un sistema de desaparición o “vida útil” para las partículas. Esto es intencional para mantener el efecto visual de la obra: los trazos de las partículas se acumulan en el lienzo, generando una pintura viva y en evolución constante.

Esta elección prioriza la estética y la experiencia visual sobre la optimización de memoria o rendimiento, permitiendo que la obra evolucione sin perder el historial visual de movimiento.

### 3. Enlace a la obra de arte

https://editor.p5js.org/DaviSlime/sketches/3vEPRwNWL

### 4. Codigo Fuente

```js
let pinceles = [];
let planeta;

function setup() {
  createCanvas(800, 800);
  background(0);

  // Planeta central
  planeta = new Planeta(createVector(width / 2, height / 2));

  // Crear pinceles iniciales
  for (let i = 0; i < 60; i++) {
    agregarPincel(random(width), random(height));
  }
}

function draw() {
  // No limpiamos el fondo para que las trayectorias se acumulen
  for (let p of pinceles) {
    p.atraer(planeta);
    p.update();
    p.display();
  }

  // Mostrar el planeta
  planeta.display();
}

function mousePressed() {
  // Añadir más pinceles con cada clic
  for (let i = 0; i < 10; i++) {
    agregarPincel(mouseX, mouseY);
  }
}

function agregarPincel(x, y) {
  let tipo = random(["grueso", "fino", "borroso"]);
  let p;
  if (tipo === "grueso") {
    p = new PincelGrueso(createVector(x, y));
  } else if (tipo === "fino") {
    p = new PincelFino(createVector(x, y));
  } else {
    p = new PincelBorroso(createVector(x, y));
  }
  pinceles.push(p);
}

// --------------------- CLASES ---------------------

class Particle {
  constructor(pos) {
    this.pos = pos.copy();
    this.vel = p5.Vector.random2D().mult(random(0.5, 2));
    this.acc = createVector(0, 0);
    this.mass = random(1, 3);
    this.prevPos = this.pos.copy();
    this.color = color(random(100, 255), random(100, 255), random(100, 255), 100);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acc.add(f);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  atraer(planeta) {
    let force = p5.Vector.sub(planeta.pos, this.pos);
    let d = constrain(force.mag(), 10, 50);
    force.normalize();
    let G = 2;
    let strength = (G * this.mass * planeta.mass) / (d * d);
    force.mult(strength);
    this.applyForce(force);
  }

  display() {
    // Se sobrescribe en subclases
  }
}

class Planeta {
  constructor(pos) {
    this.pos = pos.copy();
    this.mass = 1000;
    this.r = 40;
  }

  display() {
    push();
    noStroke();
    for (let r = this.r * 2; r > 0; r -= 2) {
      let alpha = map(r, 0, this.r * 2, 255, 0);
      fill(80, 120, 255, alpha);
      ellipse(this.pos.x, this.pos.y, r * 2);
    }
    pop();
  }
}

// -------- SUBCLASES DE PINCEL --------

class PincelGrueso extends Particle {
  display() {
    stroke(this.color);
    strokeWeight(6);
    line(this.prevPos.x, this.prevPos.y, this.pos.x, this.pos.y);
    this.prevPos = this.pos.copy();
  }
}

class PincelFino extends Particle {
  display() {
    stroke(this.color);
    strokeWeight(2);
    line(this.prevPos.x, this.prevPos.y, this.pos.x, this.pos.y);
    this.prevPos = this.pos.copy();
  }
}

class PincelBorroso extends Particle {
  display() {
    stroke(red(this.color), green(this.color), blue(this.color), 40);
    strokeWeight(3);
    line(this.prevPos.x, this.prevPos.y, this.pos.x, this.pos.y);
    this.prevPos = this.pos.copy();
  }
}
```

### Evidencia
<img width="800" height="798" alt="image" src="https://github.com/user-attachments/assets/40e01d81-d727-4765-9fea-d887d15674ef" />


### Ejemplo 4.6: a Particle System with Forces.

### 1. Gestión de partículas y memoria
Cada clic genera un nuevo sistema de partículas con color único, almacenado en un arreglo.  
Cuando una partícula pierde su vida útil, se elimina del arreglo, liberando memoria.  
Si se presiona la barra espaciadora, se borran todos los sistemas.

### 2. Conceptos aplicados
- **Particle System with Forces (Cap. 4.6):** las partículas se ven afectadas por fuerzas como gravedad, fuerzas centrípetas y de giro.  
- **Springs (Cap. 3):** las partículas están conectadas con resortes que generan oscilaciones naturales.  

### 3. Enlace a la obra

https://editor.p5js.org/DaviSlime/sketches/5g0QVD0Pj

### 4. Codigo

```js
// --- Sistema de partículas con resortes y fuerzas giratorias ---
// Basado en "The Nature of Code" (Cap 3 y 4)

let systems = [];

function setup() {
  createCanvas(900, 600);
  background(15);
}

function draw() {
  background(15, 40); // Fondo con efecto "trailing"

  for (let ps of systems) {
    ps.applyGlobalForces();
    ps.run();
  }
}

// Clic: crear un nuevo sistema de partículas en la posición del mouse
function mousePressed() {
  let ps = new ParticleSystem(createVector(mouseX, mouseY));
  systems.push(ps);
}

// Barra espaciadora: borrar todos los sistemas
function keyPressed() {
  if (key === ' ') {
    systems = [];
  }
}

// ---------------- Clases ----------------

class Particle {
  constructor(position, col) {
    this.pos = position.copy();
    this.vel = p5.Vector.random2D().mult(random(1, 2));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.col = col; // color propio
  }

  applyForce(force) {
    this.acc.add(force);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.lifespan -= 1.0;
  }

  display() {
    stroke(this.col.levels[0], this.col.levels[1], this.col.levels[2], this.lifespan);
    strokeWeight(2);
    fill(this.col.levels[0], this.col.levels[1], this.col.levels[2], this.lifespan);
    ellipse(this.pos.x, this.pos.y, 8);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

class ParticleSystem {
  constructor(origin) {
    this.origin = origin.copy();
    this.particles = [];

    // Color random único para este sistema
    this.col = color(random(100, 255), random(100, 255), random(100, 255));

    // Crear partículas iniciales
    for (let i = 0; i < 8; i++) {
      this.particles.push(new Particle(this.origin, this.col));
    }

    // Crear "resortes" (pares de partículas unidas)
    this.springs = [];
    for (let i = 0; i < this.particles.length; i++) {
      let a = this.particles[i];
      let b = this.particles[(i + 1) % this.particles.length]; // circular
      this.springs.push(new Spring(a, b, 50, this.col));
    }
  }

  applyGlobalForces() {
    for (let p of this.particles) {
      // Gravedad ligera
      let gravity = createVector(0, 0.03);
      p.applyForce(gravity);

      // Fuerza centrípeta (como un remolino)
      let dir = p5.Vector.sub(this.origin, p.pos);
      dir.normalize();
      dir.mult(0.05);
      p.applyForce(dir);

      // Fuerza de "spinning"
      let spin = createVector(-dir.y, dir.x).mult(0.05);
      p.applyForce(spin);
    }
  }

  run() {
    // Actualizar resortes
    for (let s of this.springs) {
      s.update();
      s.display();
    }

    // Actualizar partículas
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.update();
      p.display();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

class Spring {
  constructor(a, b, restLength, col) {
    this.a = a;
    this.b = b;
    this.k = 0.05; // constante del resorte
    this.restLength = restLength;
    this.col = col; // mismo color que las partículas del sistema
  }

  update() {
    let force = p5.Vector.sub(this.b.pos, this.a.pos);
    let d = force.mag();
    let stretch = d - this.restLength;

    // Hooke's law: F = -k * stretch
    force.normalize();
    force.mult(-1 * this.k * stretch);

    this.a.applyForce(force);
    force.mult(-1);
    this.b.applyForce(force);
  }

  display() {
    stroke(this.col);
    line(this.a.pos.x, this.a.pos.y, this.b.pos.x, this.b.pos.y);
  }
}

```

### 5. Evidencia

<img width="888" height="741" alt="image" src="https://github.com/user-attachments/assets/18bccf08-904c-45cd-b1df-3fb8d9bafedc" />


## Ejemplo 4.7: a Particle System with a Repeller.

### 1. Gestión de la creación, desaparición de partículas y memoria
Las partículas se crean en cada frame en el sistema, y se van eliminando automáticamente cuando su vida llega a cero. Esto evita que se acumulen infinitamente y asegura que la memoria se gestione de forma eficiente, manteniendo la simulación fluida.

### 2. Conceptos aplicados
- **Particle System con Repeller (Cap. 4.7):** Usamos partículas que reaccionan a fuerzas de repulsión, simulando el efecto de las "flores" alejándose de los puntos repelentes.  
- **Forces (Cap. 2):** Aplicamos vectores de fuerza para controlar movimiento y dirección.  
- **Motion 101 (Cap. 1):** Cada partícula sigue reglas básicas de movimiento (posición, velocidad, aceleración).

### 3. Enlace a la obra

https://editor.p5js.org/DaviSlime/sketches/zly7b0ap0

### 4. Codigo

```js
// --- Jardín de partículas solares con Repellers dinámicos ---
// Basado en "The Nature of Code" (Cap. 1 a 4)

let systems = [];
let repellers = [];

function setup() {
  createCanvas(900, 600);
  background(20);
  
  // Un par de repulsores iniciales
  repellers.push(new Repeller(width * 0.3, height * 0.5));
  repellers.push(new Repeller(width * 0.7, height * 0.4));
}

function draw() {
  background(20, 40); // efecto trailing

  // Dibujar y mover repulsores
  for (let r of repellers) {
    r.move();
    r.display();
  }

  // Actualizar sistemas de partículas
  for (let ps of systems) {
    for (let r of repellers) {
      ps.applyRepeller(r);
    }
    ps.run();
  }
}

// --- Control de mouse ---
function mousePressed() {
  if (mouseButton === LEFT) {
    // Clic izquierdo -> nueva flor
    systems.push(new ParticleSystem(createVector(mouseX, mouseY)));
  } else if (mouseButton === RIGHT) {
    // Clic derecho -> nuevo repulsor
    repellers.push(new Repeller(mouseX, mouseY));
    return false; // evita menú contextual
  }
}

// Barra espaciadora: limpiar todo
function keyPressed() {
  if (key === ' ') {
    systems = [];
    repellers = [];
  }
}

// ---------------- Clases ----------------

// Partícula individual
class Particle {
  constructor(position, col) {
    this.pos = position.copy();
    this.vel = p5.Vector.random2D().mult(random(1, 3));
    this.acc = createVector(0, 0);
    this.lifespan = 255;
    this.col = col;
    this.theta = random(TWO_PI); // para oscilación
  }

  applyForce(force) {
    this.acc.add(force);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // Oscilación suave
    this.theta += 0.1;
    this.pos.x += sin(this.theta) * 0.5;

    this.lifespan -= 1.5;
  }

  display() {
    noStroke();
    fill(this.col.levels[0], this.col.levels[1], this.col.levels[2], this.lifespan);
    ellipse(this.pos.x, this.pos.y, 8);
  }

  isDead() {
    return this.lifespan < 0;
  }
}

// Sistema de partículas ("flor")
class ParticleSystem {
  constructor(origin) {
    this.origin = origin.copy();
    this.particles = [];

    // color único para la flor
    this.col = color(random(150, 255), random(100, 200), random(100, 255));

    // generar pétalos iniciales
    for (let i = 0; i < 20; i++) {
      this.particles.push(new Particle(this.origin, this.col));
    }
  }

  applyRepeller(repeller) {
    for (let p of this.particles) {
      let force = repeller.repel(p);
      p.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.update();
      p.display();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// Repulsor (simula ráfaga de viento)
class Repeller {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.power = 100;
    this.angle = random(TWO_PI);
    this.speed = random(0.01, 0.03); // movimiento lento
  }

  repel(particle) {
    let dir = p5.Vector.sub(this.pos, particle.pos);
    let d = dir.mag();
    d = constrain(d, 5, 100);
    dir.normalize();
    let force = -1 * this.power / (d * d);
    dir.mult(force);
    return dir;
  }

  move() {
    // Movimiento circular suave
    this.angle += this.speed;
    this.pos.x += cos(this.angle) * 0.3;
    this.pos.y += sin(this.angle) * 0.3;
  }

  display() {
    noFill();
    stroke(100, 200, 255, 180);
    ellipse(this.pos.x, this.pos.y, 30);
  }
}

```

### 5. Evidencia

<img width="875" height="742" alt="image" src="https://github.com/user-attachments/assets/8eba18b0-3f4f-4669-8bd8-48ce69707b2a" />

