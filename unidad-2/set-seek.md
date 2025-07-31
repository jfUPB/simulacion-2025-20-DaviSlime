# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 1

En esta actividad vamos a repasar algunos conceptos básicos de los vectores. Te propondré que analicemos juntos algunos de los ejemplos del texto de guía.

  - ¿Cómo funciona la suma dos vectores en p5.js?

La suma de vectores funciona sumando un vector y donde este finalice se comienza el otro vector y ese resultado desde l cola inicial hasta la cabeza de la segunda da la suma
<img width="446" height="420" alt="image" src="https://github.com/user-attachments/assets/c2b11724-ab39-4760-8928-a15354f11420" />


  - ¿Por qué esta línea position = position + velocity; no funciona?

porque no esta sobrecargada como en otros lenguajes es decir no esta configurado para sumar vectores

### Actividad 2

#### Realiza este ejercicio del libro Exercise 1.1

  - ¿Qué tuviste que hacer para hacer la conversión propuesta?
cambiar las dos posiciones x y por un createVector y todas las posiciones se pe ponen la posicion (pos). 

- Muestra el código que utilizaste para resolver el ejercicio.

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
    this.pos = createVector(width / 2, height / 2);
  }

  show() {
    stroke(0);
    point(this.pos.x, this.pos.y);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.pos.x++;
    } else if (choice == 1) {
      this.pos.x--;
    } else if (choice == 2) {
      this.pos.y++;
    } else {
      this.pos.y--;
    }
  }
}


```

### Actividad 3

```javascript
let position;

function setup() {
    createCanvas(400, 400);
    posicion = createVector(6,9);
    console.log(posicion.toString());
    playingVector(posicion);
    console.log(posicion.toString());
    noLoop();
}

function playingVector(v){
    v.x = 20;
    v.y = 30;
}

function draw() {
    background(220);
    console.log("Only once");
}
```

#### *¿Qué resultado esperas obtener en el programa anterior?*
espero obtener un resultado donde me muestre los dos vectores el vector (6,9) y el vector (20,30) ademas de que al final dice "only once"

#### *¿Qué resultado obtuviste?*
el resultado fue en un 90% como pense pero le añadió un eje mas el z es decir (6,9,0) y (20,30,0) fue interesante

#### *Recuerda los conceptos de paso por valor y paso por referencia en programación. Muestra ejemplos de este concepto en javascript.*

Cuando pasamos tipos primitivos (como number, string, boolean), se pasa una copia del valor, no el original. Ejemplo:

```javascript

let x = 10;

function cambiarValor(a) {
  a = 20;
}

cambiarValor(x);
console.log(x);  // Imprime 10

```

El valor original de x no cambia porque se pasa por valor.


#### *¿Qué tipo de paso se está realizando en el código?*

Se está realizando un paso por referencia, ya que p5.Vector es un objeto.
Cuando se pasa a la función playingVector(v), se modifica el mismo vector que está en posicion.

#### *¿Qué aprendiste?*

  * Que los objetos en JavaScript se pasan por referencia, por lo que pueden ser modificados desde funciones.
  * Que al modificar los valores de un vector dentro de una función, se está afectando directamente el objeto original.
 

### Actividad 4

#### *¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?*

El método mag() calcula la magnitud o longitud de un vector, es decir, qué tan largo es. Es como medir la distancia desde el origen hasta la posición del vector en el espacio. magSq() devuelve la magnitud al cuadrado del vector, sin calcular la raíz cuadrada. Es más eficiente que mag() porque evita una operación matemática costosa (la raíz cuadrada). Si solo necesitas comparar magnitudes (por ejemplo, para saber cuál vector es más largo), magSq() es preferible.

#### *¿Para qué sirve el método normalize()?*

normalize() convierte el vector en un vector unitario, es decir, un vector con la misma dirección pero con magnitud igual a 1. Esto es útil cuando te importa la dirección pero no la magnitud, como en movimientos o direcciones de fuerza.

#### *Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?*

El método dot() mide cuánto apuntan dos vectores en la misma dirección: sirve para calcular el ángulo entre ellos o saber si van en la misma o en direcciones opuestas.

#### *El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?*

La versión de instancia se llama desde un objeto vector y se le pasa otro vector como argumento: a.dot(b).
La versión estática se llama desde la clase y toma dos vectores como argumentos: p5.Vector.dot(a, b). Ambas hacen lo mismo, pero se usan de forma diferente según el contexto.

#### *Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.*

El producto cruz (cross product) entre dos vectores genera un nuevo vector que es perpendicular (ortogonal) a ambos vectores originales.

* Magnitud: representa el área del paralelogramo que forman los dos vectores.

* Orientación: sigue la regla de la mano derecha, lo que significa que apunta hacia afuera de la superficie si enrollas los dedos de tu mano derecha desde el primer vector hacia el segundo.

#### *¿Para que te puede servir el método dist()?*

El método dist() calcula la distancia entre dos vectores, que se interpreta como la distancia entre dos puntos en el espacio. Es útil para saber cuán lejos está un objeto de otro.

#### *¿Para qué sirven los métodos normalize() y limit()?*

* normalize() convierte el vector en una dirección pura (magnitud 1), útil para mantener direcciones consistentes sin importar la fuerza.

* limit() restringe la magnitud de un vector a un máximo dado, lo cual es útil para controlar velocidades máximas, evitar que objetos se muevan demasiado rápido, etc.

* 

