# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 1
El sistema aleatorio principalmente es una forma de hacer unica la experiencia.

Frase: Cada obra es unica

### Actividad 2
Sofia nos presentó un proyecto de arte generativo con una aleatoriedad basado en raices que seguia la musica esto al momento de verlo se puede sentir que es unica ademas de que tambien depente de la persona que toque el arte generativo en la cancion puede editar el comportamiento segun como el lo vea mejor eto hace unico el arte generativo y nos permite ver tambien la vision de quien lo toca.

En mi campo puedo aplicar la aleatoriedad cuando voy a elegir los colores podemos hacerlo de forma aleatoria y generar algo interesante

### Actividad 3

#### Realiza el siguiente experimento y reporta los resultados en tu bitácora:

- Modifica el código del ejemplo Example 0.1: A Traditional Random Walk.
- Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.
   -  Espero generar 5 walks con colores diferentes y que cada vez que toquen un color que no es el suyo este cambie de color
- Ejecuta el código y escribe en tu bitácora qué sucedió realmente.
   - Lo que paso en verdad es que si generó los 5 walks pero solo cambiaba de color cada vez que chocaba con la cabeza del otro walk no cada vez que tocaba otro color
- Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?
   - parcialmente si funcionó pero hice el codigo para que cambiara el color cuando se encontrara con otro walk, no cuando encontrara otro color.
### Codigo original:

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

Codigo con cambios:

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


