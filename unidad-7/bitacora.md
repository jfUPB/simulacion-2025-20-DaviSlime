# Evidencias de la unidad 7


## Actividad 1


**Conexion con la palabra**
- "Shark"
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/e7e8f58d-118d-4bef-bb93-40caa5e1962e" />

La imagen muestra clasramente la silueta de un tiburon como es la palabra pero formado por las letras de su nombre me parece una idea genial y muy creativa.

- "Insomnia"

  <img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/ea8531df-99a2-45ec-b7cd-e4ae5b5b2286" />

Me parece una idea muy increible jugar con las sombras y las luses para hacer una representacion grafica de lo que es el insomnio.
  
- "Magnetism"
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/de1327df-9b35-47aa-aa0c-3b6e8e4d39a4" />

Es una manera muy ingeniosa de representar los dos polos opuestos del magnetismo el "+" y "-" como la t y la i es muy bonito y se entiende claramente.


**Mis propias ideas:**

- **“Suspenso”**
Idea: cada letra cuelga de un hilo invisible, oscilando, golpeándose ligeramente unas con otras; con gravedad y tensión, hasta que al final caen o se alinean.

- **“Inercia”**
Idea: una letra inicial recibe impulso horizontal, choca contra otra, la empuja, y así sucesivamente — la palabra se “propaga” por transferencia de movimiento.

- **“Inercia”**
Idea: la palabra se disuelve en pequeños granos de arena


## Actividad 2

**1. Muestra el código de los dos (o más) experimentos básicos que replicaste integrando Matter.js y p5.js.**

```js
const { Engine, Render, World, Bodies, Body, Mouse, MouseConstraint, Composite } = Matter;

let engine;
let world;
let boxes = [];
let circles = [];
let ground;
let mConstraint;

function setup() {
  createCanvas(800, 600);
  engine = Engine.create();
  world = engine.world;
  world.gravity.y = 1; // gravedad hacia abajo

  // Crear plataforma en la parte inferior
  ground = Bodies.rectangle(width / 2, height - 20, width, 40, {
    isStatic: true,
    render: { fillStyle: 'black' }
  });
  World.add(world, ground);

  // Configurar interacción del mouse
  const canvasMouse = Mouse.create(canvas.elt);
  canvasMouse.pixelRatio = pixelDensity();

  mConstraint = Matter.MouseConstraint.create(engine, {
    mouse: canvasMouse,
    constraint: {
      stiffness: 0.2,
      render: { visible: false }
    }
  });
  World.add(world, mConstraint);
}

function draw() {
  background(220);
  Engine.update(engine);

  // Dibujar la plataforma
  fill(100);
  drawVertices(ground.vertices);

  // Dibujar cuadrados
  for (let box of boxes) {
    fill(200, 100, 100);
    drawVertices(box.vertices);
  }

  // Dibujar círculos
  for (let circle of circles) {
    fill(100, 100, 200);
    drawCircle(circle);
  }
}

// Teclas para crear objetos
function keyPressed() {
  if (key === 'a' || key === 'A') {
    let box = Bodies.rectangle(random(100, width - 100), 50, 40, 40);
    boxes.push(box);
    World.add(world, box);
  } else if (key === 's' || key === 'S') {
    let circle = Bodies.circle(random(100, width - 100), 50, 20);
    circles.push(circle);
    World.add(world, circle);
  }
}

// Función para dibujar vértices (cuadrados o polígonos)
function drawVertices(vertices) {
  beginShape();
  for (let v of vertices) {
    vertex(v.x, v.y);
  }
  endShape(CLOSE);
}

// Función para dibujar círculos
function drawCircle(body) {
  const pos = body.position;
  const r = body.circleRadius;
  ellipse(pos.x, pos.y, r * 2);
}

```



**2. Incluye una captura de pantalla o ENLACE a un GIF (no olvides, enlace) de cada experimento funcionando.**


https://github.com/user-attachments/assets/a3c34899-4ea0-4da0-ae4e-89345c50e460


**Qué hace este código?**

**Gravedad:** Se define con world.gravity.y = 1, lo cual aplica gravedad vertical hacia abajo.

**Plataforma visible:** Se crea un rectángulo estático en la parte inferior como el suelo.

**Teclas:**

"a" crea un cuadrado que cae.

"s" crea un círculo que también cae.

**Colisiones:** Todos los cuerpos tienen colisiones por defecto en Matter.js.

**Interacción con mouse:**

Se usa MouseConstraint de Matter.js para que puedas arrastrar con el botón izquierdo del mouse cualquier objeto físico (círculo o cuadrado).

**3. Proporciona tu explicación clara y concisa de los conceptos clave (Engine, World, Bodies, Constraint, MouseConstraint).**

- Engine: Es el motor para la simulacion de fisicas que se vaya a usar.
- World: Es el lugar donde se almacenan todos los objetos, cuerpos, constrains y todos los elemento que estan en la simulación.
- Bodies: Es un nombre lara crear bodies con caracteriticas especificas con atributos preseteados que se puedan duplicar.
- Constraint: Es una linea que conecta un bodie con otro y tienen rigidez para que se mantengan juntas o no.
- Mouse Constraint: Es lo mismo que el contraint pero en vez de que sea un body con otro es con el mouse.

**4. Menciona brevemente cualquier dificultad encontrada al configurar o usar Matter.js inicialmente.**

**Separación entre física y renderizado:** Matter.js maneja la física, pero no dibuja nada. Hay que usar p5.js para representar los objetos en pantalla manualmente con ellipse() o beginShape(), lo cual no es inmediato para quienes vienen de otras librerías más integradas.

**Coordinación del mouse con el mundo físico:** Para interactuar con los objetos con el mouse, hay que usar MouseConstraint, y configurarlo correctamente requiere enlazarlo con el canvas.elt y ajustar el pixelDensity(), lo que no es obvio al principio.


## Actividad 3

**1. **Indica claramente la palabra elegida.****
  La palabra elegida es "Sand" arena en inglés

**2. Idea conceptual: ¿Cómo la animación física representa el significado de la palabra?**

La palabra “Sand” (arena) está construida visualmente como una forma sólida y clara, pero en realidad está compuesta por miles de pequeñas partículas que simulan granos de arena. Al presionar la tecla “a”, esta estructura aparentemente firme se desintegra y cae por acción de la gravedad, como si fuera arena real. Este colapso visual refleja el significado literal y físico de la palabra: algo frágil, granular y moldeado por la gravedad, reforzando el concepto de “Word as Image” donde la palabra actúa como lo que representa.

**3. Aspectos técnicos clave de la implementación**

- Las letras no se formaron con cuerpos rígidos de Matter.js, sino con partículas individuales colocadas según la forma de la palabra renderizada en un canvas auxiliar.

- Cada partícula es un cuerpo circular de Matter.js, inicialmente fijo (sin física) y luego liberado para caer.

- Las propiedades físicas clave fueron:

  - Gravedad para simular la caída.

  - Colisiones para que los granos interactúen y se acumulen.

  - Fricción y restitución (rebote bajo) para simular el comportamiento de arena.

4. Incluye el código completo de tu sketch final.

```js
// Matter.js
let Engine = Matter.Engine,
    World = Matter.World,
    Bodies = Matter.Bodies;

let engine, world;

let particles = [];
let font;
let pg;

let released = false;
let ground;

function preload() {
  font = loadFont('https://cdnjs.cloudflare.com/ajax/libs/topcoat/0.8.0/font/SourceCodePro-Regular.otf');
}

function setup() {
  createCanvas(800, 400);
  engine = Engine.create();
  world = engine.world;
  world.gravity.y = 1;

  pg = createGraphics(width, height);
  pg.pixelDensity(1);
  pg.background(0, 0);
  pg.textFont(font);
  pg.textSize(200);
  pg.fill(220, 200, 160); // color arena
  pg.textAlign(CENTER, CENTER);
  pg.text('SAND', width / 2, height / 2);
  pg.loadPixels();

  let density = 4; // menor = más partículas
  for (let x = 0; x < pg.width; x += density) {
    for (let y = 0; y < pg.height; y += density) {
      let index = (x + y * pg.width) * 4;
      let alpha = pg.pixels[index + 3];
      if (alpha > 128) {
        let col = color(
          220 + random(-10, 10),
          200 + random(-10, 10),
          160 + random(-10, 10)
        );
        particles.push(new SandParticle(x, y, density / 2, col));
      }
    }
  }

  // Ground for particles to fall onto
  ground = Bodies.rectangle(width / 2, height + 25, width, 50, {
    isStatic: true,
    render: { visible: false }
  });
  World.add(world, ground);
}

function draw() {
  background(250, 245, 230); // fondo suave arena

  Engine.update(engine);

  for (let p of particles) {
    p.show();
  }
}

function keyPressed() {
  if (key === 'a' || key === 'A') {
    releaseParticles();
  }
}

function releaseParticles() {
  if (released) return;
  released = true;
  for (let p of particles) {
    p.release();
  }
}

// Clase para cada partícula
class SandParticle {
  constructor(x, y, r, c) {
    this.x = x;
    this.y = y;
    this.r = r;
    this.c = c;
    this.released = false;
    this.body = null;
  }

  release() {
    if (!this.released) {
      this.body = Bodies.circle(this.x, this.y, this.r, {
        restitution: 0.1,
        friction: 0.2,
        frictionAir: 0.02
      });
      World.add(world, this.body);
      this.released = true;
    }
  }

  show() {
    noStroke();
    fill(this.c);
    if (this.released && this.body) {
      let pos = this.body.position;
      push();
      translate(pos.x, pos.y);
      ellipse(0, 0, this.r * 2);
      pop();
    } else {
      ellipse(this.x, this.y, this.r * 2);
    }
  }
}

```

5. Inserta una captura de pantalla estática Y un enlace a un GIF animado (¡Esencial!) que muestre tu tipografía semántica animada en acción.



https://github.com/user-attachments/assets/f2e42a9a-eea5-42c6-9b2b-a5a11906ff72



## Autoevaluación

5.0 Ya que cumpli con todos los requerimientos para poder merecerme esta nota, es decir, realicé las 3 actividades completas y la autoevaluación. jeje
