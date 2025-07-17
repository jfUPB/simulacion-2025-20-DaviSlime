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
- Ejecuta el código y escribe en tu bitácora qué sucedió realmente.
- Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?

´// The Nature of Code
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
´
