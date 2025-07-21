# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 1
El sistema aleatorio principalmente es una forma de hacer unica la experiencia.

Frase: Cada obra es unica

### Actividad 2
Sofia nos presentó un proyecto de arte generativo con una aleatoriedad basado en raices que seguia la musica esto al momento de verlo se puede sentir que es unica ademas de que tambien depente de la persona que toque el arte generativo en la cancion puede editar el comportamiento segun como el lo vea mejor eto hace unico el arte generativo y nos permite ver tambien la vision de quien lo toca.

En mi campo puedo aplicar la aleatoriedad cuando voy a elegir los colores podemos hacerlo de forma aleatoria y generar algo interesante

### Actividad 3

#### Caminatas aleatorias

Realiza el siguiente experimento y reporta los resultados en tu bitácora:

- Modifica el código del ejemplo Example 0.1: A Traditional Random Walk.
- Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.
   -  Espero generar 5 walks con colores diferentes y que cada vez que toquen un color que no es el suyo este cambie de color
- Ejecuta el código y escribe en tu bitácora qué sucedió realmente.
   - Lo que paso en verdad es que si generó los 5 walks pero solo cambiaba de color cada vez que chocaba con la cabeza del otro walk no cada vez que tocaba otro color
- Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?
   - parcialmente si funcionó pero hice el codigo para que cambiara el color cuando se encontrara con otro walk, no cuando encontrara otro color.
#### Codigo original:

```javascript
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

#### Codigo con cambios:

```javascript
let walkers = [];

function setup() {
  createCanvas(600, 600);
  background(255); // fondo blanco

  // Crear 5 walkers en el centro con colores aleatorios
  for (let i = 0; i < 5; i++) {
    walkers.push(new Walker(width / 4, height / 4));
  }

  strokeWeight(5); // tamaño del punto
}

function draw() {
  for (let w of walkers) {
    w.step();
    w.display();
  }
}

class Walker {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    this.color = this.randomColor();
  }

  randomColor() {
    return color(random(255), random(255), random(255));
  }

  step() {
    // Movimiento aleatorio en X e Y con igual probabilidad
    this.x += random([-1, 0, 1]);
    this.y += random([-1, 0, 1]);

    // Limita al canvas
    this.x = constrain(this.x, 0, width - 1);
    this.y = constrain(this.y, 0, height - 1);

    // Obtener el color actual del píxel
    let pixelColor = get(this.x, this.y);
    let currentColor = [red(this.color), green(this.color), blue(this.color)];

    // Si el color del píxel es distinto al que pinta el walker, cambia de color
    if (!this.colorsAreSimilar(pixelColor, currentColor, 10)) {
      this.color = this.randomColor();
    }
  }

  colorsAreSimilar(c1, c2, tolerance) {
    // Compara RGB uno por uno
    for (let i = 0; i < 3; i++) {
      if (abs(c1[i] - c2[i]) > tolerance) {
        return false;
      }
    }
    return true;
  }

  display() {
    stroke(this.color);
    point(this.x, this.y);
  }
}


```


### Actividad 4

#### Distribuciones de probabilidad

En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.
- La diferencia es que la distribucion uniforme tienen la misma aleatoriedad es decir la misma probabilidad para todas las diferentes opciones disponibles pero la no uniforme favorece mas a ciertas opciones especificas que tienen una probabilidad mas alta de ser escogidos.

Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.

 ```javascript
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.x, this.y);
  }

  step() {
    const choice = random( 10);
    if (choice <=6) {
      this.x++;
    } else if (choice <= 7) {
      this.x--;
    } else if (choice <= 8) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
  ```

### Actividad 5

Una vez has entendido el concepto de distribución normal, vas a pensar en una nueva manera de visualizarlo.

* Crea un nuevo sketch en p5.js que represente una distribución normal.
* Copia el código en tu bitácora.
* Coloca en enlace a tu sketch en p5.js en tu bitácora.
* Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.

```javascript
let bins;
let numBins = 60;
let values = [];

function setup() {
  createCanvas(600, 400);
  bins = new Array(numBins).fill(0);
  background(255);
}

function draw() {
  // Generar valores con distribución normal
  let val = randomGaussian(width / 2, 60);
  values.push(val);

  // Llenar histogramas (barras)
  let index = floor(map(val, 0, width, 0, numBins));
  if (index >= 0 && index < numBins) {
    bins[index]++;
  }

  // Dibujar fondo y ejes
  background(255);
  stroke(0);
  fill(0);
  textAlign(CENTER);
  line(0, height - 20, width, height - 20); // eje x

  // Dibujar barras
  let barWidth = width / numBins;
  for (let i = 0; i < bins.length; i++) {
    let h = map(bins[i], 0, max(bins), 0, height - 50);
    fill(100, 180, 255);
    rect(i * barWidth, height - 20 - h, barWidth - 1, h);
  }

  // Detener cuando hay suficientes datos
  if (values.length > 2000) {
    noLoop();
  }
}

```

<img width="747" height="479" alt="image" src="https://github.com/user-attachments/assets/dd6d665f-2ad3-4c9d-8350-ce36c5c25bde" />


Link p5.js: [https://editor.p5js.org/DaviSlime/sketches/0iFfuzHky](https://editor.p5js.org/DaviSlime/sketches/blwreXATH)

### Actividad 6

Ahora vas a:

* Crea un nuevo sketch en p5.js donde modifiques uno de los ejemplos anteriores y adiciones de Lévy flight.
* Explica por qué usaste esta técnica y qué resultados esberabas obtener.
* Copia el código en tu bitácora.
* Coloca en enlace a tu sketch en p5.js en tu bitácora.
* Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.

```javascript
let binsNormal;
let binsLevy;
let numBins = 60;
let valuesNormal = [];
let valuesLevy = [];

function setup() {
  createCanvas(800, 400);
  binsNormal = new Array(numBins).fill(0);
  binsLevy = new Array(numBins).fill(0);
  background(255);
}

function draw() {
  // --- Distribución Normal
  let valNormal = randomGaussian(width / 4, 40);
  valuesNormal.push(valNormal);
  let indexNormal = floor(map(valNormal, 0, width / 2, 0, numBins));
  if (indexNormal >= 0 && indexNormal < numBins) {
    binsNormal[indexNormal]++;
  }

  // --- Lévy Flight
  let step = pow(random(1), -1.5); // potencia para hacer pasos largos ocasionalmente
  let direction = random([1, -1]);
  let valLevy = width * 0.75 + direction * step * 10;
  valuesLevy.push(valLevy);
  let indexLevy = floor(map(valLevy, width / 2, width, 0, numBins));
  if (indexLevy >= 0 && indexLevy < numBins) {
    binsLevy[indexLevy]++;
  }

  background(255);
  stroke(0);
  fill(0);
  textAlign(CENTER);
  text("Distribución Normal", width / 4, 20);
  text("Lévy Flight", width * 0.75, 20);

  // Dibujar histogramas
  let barWidth = (width / 2) / numBins;

  // Normal
  for (let i = 0; i < binsNormal.length; i++) {
    let h = map(binsNormal[i], 0, max(binsNormal), 0, height - 50);
    fill(100, 180, 255);
    rect(i * barWidth, height - 20 - h, barWidth - 1, h);
  }

  // Lévy
  for (let i = 0; i < binsLevy.length; i++) {
    let h = map(binsLevy[i], 0, max(binsLevy), 0, height - 50);
    fill(255, 100, 150);
    rect(width / 2 + i * barWidth, height - 20 - h, barWidth - 1, h);
  }

  // Detener cuando haya suficientes datos
  if (valuesNormal.length > 2000 && valuesLevy.length > 2000) {
    noLoop();
  }
}

```
<img width="911" height="471" alt="image" src="https://github.com/user-attachments/assets/537d692c-bad0-44a7-8c12-fac3c6120c09" />

*P5.js:* https://editor.p5js.org/DaviSlime/sketches/0iFfuzHky


Usé esta tecnica para comparar visualmente dos comportamientos de movimiento aleatorio:

* El de la distribución normal (valores concentrados en el centro).

* El de Lévy flight (valores con más dispersión, con saltos extremos).

Quería mostrar que mientras la curva normal forma una campana simétrica, Lévy produce una distribución más ancha y con colas largas, reflejando una mayor probabilidad de eventos extremos

### Actividad 7


```javascript
let yoff = 0;

function setup() {
  createCanvas(600, 400);
  background(0);
}

function draw() {
  background(0);
  stroke(0, 255, 150); // Color verde brillante
  strokeWeight(2);
  noFill();

  beginShape();
  let xoff = 0;
  for (let x = 0; x < width; x += 8) {
    // Rango más amplio para vibración más agresiva
    let y = map(noise(xoff, yoff), 0, 1, 50, 350);
    vertex(x, y);
    xoff += 0.15; // Mayor frecuencia = más picos por línea
  }
  endShape();

  yoff += 0.05; // Mayor velocidad de cambio
}

```

<img width="750" height="498" alt="image" src="https://github.com/user-attachments/assets/7bda9940-c28f-4c5d-8dae-56991ee399c1" />

*P5.js:* https://editor.p5js.org/DaviSlime/sketches/zu3ULmc3Y

Esperaba obtener una onda brusca que tuviera picos y cambios abruptos a lo largo del tiempo y que fuera verde

