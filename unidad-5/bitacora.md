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
