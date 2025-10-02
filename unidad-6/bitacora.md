# Evidencias de la unidad 6


## Actividad 1

<img width="747" height="595" alt="image" src="https://github.com/user-attachments/assets/45f576f0-b6f3-4874-b443-c86b5757a581" />
<img width="752" height="743" alt="image" src="https://github.com/user-attachments/assets/c03e2902-57be-4e48-bf6d-80e7693d81e5" />

Esta imagen me inspira bastante paz y calma se ve muy smooth me dan ganas de hacer algo parecido pero que el color vaya variando de forma gradual y hacer que se sienta vivo


## Actividad 2

1. **¿Qué es una fuerza de dirección (steering force)?**

Una steering force es una fuerza que modifica la dirección de un agente para que se mueva hacia un objetivo deseado o siga un comportamiento específico. Se calcula como la diferencia entre la velocidad deseada y la velocidad actual, y se limita para mantener un movimiento realista.

3. **¿Qué diferencia tiene este tipo de fuerza con las que ya hemos estudiado en el contexto de la simulación de agentes?**

A diferencia de las fuerzas físicas (como gravedad o fricción), que actúan de forma pasiva, la steering force es intencional y proactiva: busca generar comportamientos como seguir, evitar o agruparse. Permite que los agentes tomen decisiones y se comporten de forma "inteligente".

4. **¿Qué relación tiene la steering force con Craig Reynolds y su trabajo en simulación de comportamiento animal?**

Craig Reynolds usó steering forces en su modelo de Boids para simular el comportamiento de grupos de animales (como aves o peces). Basó su algoritmo en tres reglas simples:

**Separación:** evitar chocar con otros.

**Alineación:** moverse en la misma dirección que el grupo.

**Cohesión:** mantenerse cerca del grupo.

Cada regla se implementa como una steering force individual, y al combinarse, producen comportamientos colectivos complejos y realistas.

## Actividad 3

1. **Explica brevemente la estructura de datos usada para el campo de flujo y cómo se generan sus vectores.**

El campo de flujo se almacena en un ```array``` unidimensional que contiene objetos p5.Vector. Este ```array``` representa una cuadrícula 2D conceptual, donde cada celda contiene un vector que indica la dirección del flujo en ese punto. Los vectores se generan utilizando la función ```noise()``` para obtener una variación suave de ángulos en el espacio, y se crean en el método ```init()``` o ```update()``` de la clase FlowField. Cada vector se calcula convirtiendo el valor de noise en un ángulo, que luego se transforma en un p5.Vector mediante ```fromAngle()```.

2. **Describe con tus palabras cómo un agente utiliza el campo para calcular su fuerza de dirección.**

El agente usa su posición actual para determinar qué vector del campo de flujo debe seguir. Esto se hace dividiendo sus coordenadas por la resolución de la cuadrícula y convirtiendo el resultado a enteros para indexar el array de flujo. Luego, el vector correspondiente se considera como la "velocidad deseada". La fuerza de dirección se calcula restando la velocidad actual del agente a esta velocidad deseada. Finalmente, esta fuerza se limita por la fuerza máxima (maxforce) antes de aplicarse.

3. **Lista los parámetros clave identificados (resolución, maxspeed, maxforce).**

- Resolución del campo de flujo: resolution (define el tamaño de cada celda de la cuadrícula).

- Velocidad máxima del agente: maxspeed.

- Fuerza máxima de dirección del agente: maxforce.

4. **Describe la modificación que realizaste al código y explica detalladamente el efecto que tuvo en el movimiento y comportamiento colectivo de los agentes. Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.**

Modificación: Se cambió la forma en que se generan los vectores del campo, sustituyendo el uso de noise() por una fórmula trigonométrica basada en la posición: let angle = sin(x * 0.1) + cos(y * 0.1);.

Código modificado:
```js
let angle = sin(x * 0.1) + cos(y * 0.1);
let v = p5.Vector.fromAngle(angle);
v.setMag(1);
this.field[index] = v;
```

Efecto observado: Al cambiar la generación del campo de noise() a funciones trigonométricas, los agentes comenzaron a moverse en trayectorias más regulares y repetitivas. El movimiento colectivo mostró patrones ondulados y simétricos, perdiendo la apariencia natural y orgánica del campo generado por noise. El comportamiento fue más predecible y menos caótico.


## Actividad 4

1. **Explica con tus palabras el objetivo y la lógica general de cálculo de cada una de las tres reglas de Flocking (Separación, Alineación, Cohesión).**

**Separación:**

cada boid mira a los vecinos que están muy cerca (distancia menor a un desiredSeparation), calcula el vector que lo aleja de cada vecino (posición propia − posición del vecino), lo normaliza y lo pondera inversamente por la distancia (vecinos muy cercanos empujan más). Se promedian esos vectores, se ponen a la magnitud deseada (maxspeed) y se calcula el steering como desired − velocity, limitando por maxforce. 


**Alineación**

Objetivo: ir en la misma dirección que los vecinos

promediar las velocidades de los boids dentro del radio de percepción; ese promedio se convierte en la desired direction (con magnitud maxspeed), luego steer = desired − velocity, limitado por maxforce. Si no hay vecinos cercanos, la fuerza es cero. 


**Cohesión**

Objetivo: mover al boid hacia el centro de sus vecinos para mantener el grupo unido.

promediar las posiciones de los vecinos (dentro de neighborDistance) → obtener el punto medio; usar seek(averagePos) (buscar ese punto) para generar la fuerza de cohesión, aplicando la misma fórmula de steer = desired − velocity y limitando por maxforce. 

En todos los casos la implementación usa vectores, promedios sobre vecinos dentro de un radio de percepción y la fórmula de Reynolds steer = desired − velocity seguida de límites por maxforce y maxspeed.

2. **Lista los parámetros clave identificados (radio de percepción, pesos de las reglas, maxspeed, maxforce).**

**Parámetros clave**

**Radio de percepción o neighborDistance**: el radio en el que un boid considera a otros como “vecinos”. En el ejemplo de Shiffman suele usarse 50 píxeles para align/cohesion. Afecta la escala de las interacciones: radios grandes → interacción global; radios muy pequeños → fragmentación en grupos muy pequeños. 


**desiredSeparation:** distancia a la que se activa la separación. Controla que tan cerca acepta a otros boids antes de empujar.

Pesos de las reglas (weights): multiplicadores aplicados a cada fuerza antes de applyForce, como separation.mult(1.5); alignment.mult(1.0); cohesion.mult(1.0); en el ejemplo. Cambiar estos pesos altera fuertemente el comportamiento emergente. 


**maxspeed:** velocidad máxima que un boid intenta alcanzar. Controla que tan rápido se mueven. 


**maxforce:** límite aplicado al vector de steering (cuánta aceleración/curvatura puede aplicar). Valores pequeños → movimientos suaves; valores mayores → giros bruscos.

3. **Describe la modificación que realizaste al código y explica detalladamente el efecto que tuvo en el comportamiento colectivo del enjambre (¿Se dispersan? ¿Forman grupos compactos? ¿se mueven caóticamente?). Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.**

**Modificación:**


- Desactivar la cohesión (cohesión = 0) y aumentar fuertemente la separación (peso de separación grande).

- Objetivo del experimento: ver qué pasa si los boids no intentan “ir al centro” pero sí evitan chocar entre sí, manteniendo cierta alineación.

**Detalles técnicos (valores usados):**

- separation.mult(3.5); (antes en el ejemplo ~1.5)

- alignment.mult(1.0); (se mantiene igual)

- cohesion.mult(0.0); (la anulo)

desiredSeparation aumentado a 40 (para que la separación actúe a mayor distancia que el ejemplo básico).

**Fragmento de código:**

```js
// EN LA CLASE Boid (o `Boid.prototype`)
flock(boids) {
  let separation = this.separate(boids);
  let alignment  = this.align(boids);
  let cohesion   = this.cohere(boids);

  // PESOS MODIFICADOS (experimento)
  separation.mult(3.5);  // separación muy fuerte
  alignment.mult(1.0);   // mantiene alineación normal
  cohesion.mult(0.0);    // cohesion desactivada

  this.applyForce(separation);
  this.applyForce(alignment);
  this.applyForce(cohesion);
}

// Método separate (aumenté desiredSeparation)
separate(boids) {
  let desiredSeparation = 40; // mayor distancia de rechazo
  let steer = createVector(0, 0);
  let count = 0;

  for (let other of boids) {
    let d = p5.Vector.dist(this.position, other.position);
    if ((this !== other) && (d < desiredSeparation)) {
      let diff = p5.Vector.sub(this.position, other.position);
      diff.normalize();
      diff.div(d); // ponderar por cercanía (más cercano = mayor fuerza)
      steer.add(diff);
      count++;
    }
  }

  if (count > 0) {
    steer.div(count);
    steer.setMag(this.maxspeed);
    steer.sub(this.velocity);
    steer.limit(this.maxforce);
  }
  return steer;
}

```
**qué vi al ejecutar:**

1. No se forman grupos compactos. Al anular la cohesión, los boids ya no sienten la “atracción al centro” del grupo, así que no tienden a agruparse alrededor de un centro único.

2. Tendencia a dispersarse pero con alineación local. La fuerte separación obliga a los boids a mantener distancias grandes; si la alineación sigue activa, verás trenes o bandas de boids que van en paralelo (misma dirección) pero suficientemente separados — el enjambre pierde su masa compacta y se convierte en muchas sub-líneas sueltas.

3. Mayor cobertura del canvas y comportamiento “escaso”. Con separación alta los boids ocupan más el área disponible; algunos terminan pegados a los bordes porque evitan acercarse entre sí.

4. No suele ser caótico si alignment > 0. La alineación impone coherencia direccional; si además la alineación se baja mucho (por ejemplo a 0.2), el sistema puede verse más errático/caótico: cada boid evita colisiones pero no sincroniza su dirección con los demás.

**Conclusión:** desactivar cohesion + separación alta ⇒ dispersión ordenada. Si en vez de eso pones separación extremadamente alta y quitas also alignment, obtienes comportamiento muy caótico/aleatorio y boids “rebotando” evitando unos a otros sin un rumbo común.


## Actividad 5

### ¿Que hacer?

1. Elige un tema musical que te inspire.

"ラブカ 歌いました" - Hiiragi Kirai

2. Diseña una pieza de arte generativo que utilice el algoritmo de flow fields y/o flocking.

3. Vas a visualizar el tema musical y además vas a “tocar” las visuales, es decir, tu pieza de arte debe ser interactiva y debe permitir la interpretación en tiempo real de las visuales como si fuera un instrumento más que acompaña de manera coherente el tema musical.

### Reporte

1. **Documenta todo el proceso de diseño y creación en tu bitácora, incluyendo bocetos y decisiones de diseño.**

Decidi hacer como una variacion de un doble flujo independientes entre si para mostrar una dualidad en una cancion donde yo tengo el control de cuando se muestra cada parte de la dualidad

2. **El código fuente completo de tu sketch en p5.js.**

```js
// Generativo: Flow fields + Flocking + Música con palpitación
// Autor: Adaptado con p5.js y p5.sound

let topAgents = [];
let bottomAgents = [];

let scl = 22;            
let cols, rows;
let flowTop = [], flowBottom = [];
let zTop = 0, zBottom = 5000; 
let zInc = 0.008;        

// audio
let sound = null;
let fft, amp;
let soundLoaded = false;

// UI
let fileInput, enableButton, playButton;
let playState = false;

// parámetros
const TOP_COUNT = 80;       
const BOTTOM_COUNT = 80;    

// pesos y límites
const flowWeight = 1.0;
const sepWeight = 1.6;
const desiredSeparation = 14;
const MAXSPEED = 2.0;
const MAXFORCE = 0.12;

function setup() {
  createCanvas(windowWidth, windowHeight);
  pixelDensity(1);
  cols = ceil(width / scl) + 1;
  rows = ceil(height / scl) + 1;

  for (let i = 0; i < cols * rows; i++) {
    flowTop[i] = createVector(0, 0);
    flowBottom[i] = createVector(0, 0);
  }

  for (let i = 0; i < TOP_COUNT; i++) {
    let x = random(width);
    let y = random(0, height / 2 - 2);
    topAgents.push(new Agent(x, y, [220, 40, 40], 'top'));
  }
  for (let i = 0; i < BOTTOM_COUNT; i++) {
    let x = random(width);
    let y = random(height / 2 + 2, height);
    bottomAgents.push(new Agent(x, y, [55, 120, 250], 'bottom'));
  }

  fileInput = createFileInput(handleFile, false);
  fileInput.position(10, 12);

  enableButton = createButton('Enable Audio');
  enableButton.position(fileInput.x + fileInput.width + 12, 10);
  enableButton.mousePressed(() => {
    userStartAudio().then(() => {
      console.log('Audio context enabled');
      fft = new p5.FFT(0.8, 1024);
      amp = new p5.Amplitude();
    });
  });

  playButton = createButton('Play / Pause');
  playButton.position(enableButton.x + enableButton.width + 10, 10);
  playButton.mousePressed(togglePlay);
  playButton.attribute('disabled', '');

  textFont('Arial', 12);
}

function handleFile(file) {
  if (file && file.size > 0) {
    const url = URL.createObjectURL(file.file);
    if (sound && sound.isPlaying()) {
      sound.stop();
      sound = null;
      soundLoaded = false;
    }
    loadSound(url,
      s => {
        sound = s;
        soundLoaded = true;
        playState = false;
        playButton.removeAttribute('disabled');
        if (!fft) fft = new p5.FFT(0.8, 1024);
        if (!amp) amp = new p5.Amplitude();
        console.log('Audio cargado: ', file.name);
      },
      err => {
        console.error('Error cargando audio', err);
      }
    );
  }
}

function togglePlay() {
  if (!soundLoaded) return;
  if (sound.isPlaying()) {
    sound.pause();
    playState = false;
  } else {
    sound.loop();
    playState = true;
  }
}

function draw() {
  background(18);

  noStroke();
  fill(30, 30);
  rect(0, 0, width, height / 2);
  fill(10, 10);
  rect(0, height / 2, width, height / 2);

  updateFlowFields();

  // amplitud global de la canción (para palpitación)
  let level = 0;
  if (soundLoaded && sound.isPlaying() && amp) {
    level = amp.getLevel();
  }

  const topActive = keyIsDown(65);  
  const bottomActive = keyIsDown(76); 

  for (let ag of topAgents) {
    ag.active = topActive;
    if (ag.active) {
      ag.follow(flowTop);
      let sep = ag.separate(topAgents);
      sep.mult(sepWeight);
      ag.applyForce(sep);
    } else {
      ag.vel.mult(0);
      ag.acc.mult(0);
    }
    ag.update();
    ag.show(level);
  }

  for (let ag of bottomAgents) {
    ag.active = bottomActive;
    if (ag.active) {
      ag.follow(flowBottom);
      let sep = ag.separate(bottomAgents);
      sep.mult(sepWeight);
      ag.applyForce(sep);
    } else {
      ag.vel.mult(0);
      ag.acc.mult(0);
    }
    ag.update();
    ag.show(level);
  }

  drawHUD();
}

function updateFlowFields() {
  let yOff = 0;
  for (let y = 0; y < rows; y++) {
    let xOff = 0;
    for (let x = 0; x < cols; x++) {
      let index = x + y * cols;
      let angle = noise(xOff * 0.9, yOff * 0.9, zTop) * TWO_PI * 2.5;
      let v = p5.Vector.fromAngle(angle);
      v.setMag(1);
      flowTop[index] = v;
      xOff += 0.12;
    }
    yOff += 0.12;
  }

  yOff = 100;
  for (let y = 0; y < rows; y++) {
    let xOff = 1000;
    for (let x = 0; x < cols; x++) {
      let index = x + y * cols;
      let angle = noise(xOff * 0.09, yOff * 0.09, zBottom) * TWO_PI * 3.5;
      let v = p5.Vector.fromAngle(angle);
      v.setMag(1);
      flowBottom[index] = v;
      xOff += 0.12;
    }
    yOff += 0.12;
  }

  zTop += zInc;
  zBottom += zInc * 0.8;
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  cols = ceil(width / scl) + 1;
  rows = ceil(height / scl) + 1;
  flowTop = new Array(cols * rows).fill(createVector(0, 0));
  flowBottom = new Array(cols * rows).fill(createVector(0, 0));
}

// --- Agent class ---
class Agent {
  constructor(x, y, rgbArr, side) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(0.3, 1.2));
    this.acc = createVector(0, 0);
    this.maxspeed = MAXSPEED;
    this.maxforce = MAXFORCE;
    this.colorRGB = rgbArr;
    this.side = side; 
    this.sizeBase = random(3.2, 6.2);
    this.active = false;
  }

  applyForce(f) {
    this.acc.add(f);
  }

  follow(flowArray) {
    let x = floor(constrain(this.pos.x, 0, width - 1) / scl);
    let y = floor(constrain(this.pos.y, 0, height - 1) / scl);
    let idx = x + y * cols;
    let force = flowArray[idx];
    if (!force) return;
    let desired = force.copy().mult(this.maxspeed * flowWeight);
    let steer = p5.Vector.sub(desired, this.vel);
    steer.limit(this.maxforce);
    this.applyForce(steer);
  }

  separate(others) {
    let steer = createVector(0, 0);
    let count = 0;
    for (let other of others) {
      let d = p5.Vector.dist(this.pos, other.pos);
      if (other !== this && d < desiredSeparation) {
        let diff = p5.Vector.sub(this.pos, other.pos);
        diff.normalize();
        diff.div(d); 
        steer.add(diff);
        count++;
      }
    }
    if (count > 0) {
      steer.div(count);
      steer.setMag(this.maxspeed);
      steer.sub(this.vel);
      steer.limit(this.maxforce);
    }
    return steer;
  }

  update() {
    this.vel.add(this.acc);
    this.vel.limit(this.maxspeed);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // si toca un borde → reaparece en su mitad
    if (this.pos.x < 0 || this.pos.x > width || this.pos.y < 0 || this.pos.y > height) {
      if (this.side === 'top') {
        this.pos = createVector(random(width), random(0, height / 2 - 2));
      } else {
        this.pos = createVector(random(width), random(height / 2 + 2, height));
      }
      this.vel.mult(0);
    }
  }

  show(level) {
    noStroke();
    if (!this.active) {
      fill(this.colorRGB[0], this.colorRGB[1], this.colorRGB[2], 120);
      ellipse(this.pos.x, this.pos.y, this.sizeBase * 0.8);
      return;
    }

    // Palpitar al ritmo del audio con amplitud global
    let pulse = map(level, 0, 0.3, 0.9, 2.2);  
    let size = this.sizeBase * pulse;
    let alpha = map(level, 0, 0.3, 160, 255);

    fill(this.colorRGB[0], this.colorRGB[1], this.colorRGB[2], alpha);
    ellipse(this.pos.x, this.pos.y, size);
  }
}

function drawHUD() {
  push();
  fill(255, 200);
  noStroke();
  rect(6, height - 66, 380, 56, 8);
  pop();

  fill(0);
  textAlign(LEFT, TOP);
  text("Mantén 'A' → rojos (arriba) | 'L' → azules (abajo)", 12, height - 60);
  text("Carga un audio, 'Enable Audio' y Play/Pause. Los agentes palpitan al ritmo.", 12, height - 40);
}

```

3. **Un enlace a tu sketch en el editor de p5.js.**

https://editor.p5js.org/DaviSlime/sketches/Sg8WoxC2U

4. **Capturas de pantalla mostrando tu pieza en acción.**

<img width="862" height="749" alt="image" src="https://github.com/user-attachments/assets/6eb01a55-c376-4eb7-a046-543841df1e9b" />

<img width="821" height="748" alt="image" src="https://github.com/user-attachments/assets/616ed1b7-370f-436d-baf6-41ff1790c250" />

<img width="850" height="742" alt="image" src="https://github.com/user-attachments/assets/57ed7b48-ad59-438d-b343-932f6ddb5393" />

## Autoevaluación




