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
