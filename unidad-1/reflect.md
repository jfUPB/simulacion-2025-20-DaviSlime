# Unidad 1

## 🤔 Fase: Reflect

### Actividad 9

#### Parte 1: recuperación de conocimiento (Retrieval Practice)

- Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?
    * la diferencia fundamental es que el random es una aleatoriedad pura es decir, todas las probabilidades tienen igual chance de salir y no dependen de nada externo cosa que si pasa con el noise que basicamente depende          del ruido que se haga y este afecta ligeramente el complonente aleatorio
 
- Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?
    * una distribucion de probabilidad es la forma de describir como salen los valores aleatorios dependiendo de su probabilidad especifica por ejemplo, la distribucion uniforme cada valor tiene la misma probabilidad de ser        elegido, sin embargo en la normal la probabilidad de aparecer aumenta conforme se va acercando a la media.

- ¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple
    *El papel fundamental es hacer unico cada obra o presentacion donde nunca va a suceder exactamente lo mismo dos ejemplos de esto es cuando hay cambios de color aleatorios o se modifica la velocidad de crecimiento o se         aumenta un valor por sobre otro.

- Piensa en tu obra final (Actividad 08). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.
    *En mi obra usé la distribucion uniforme para que se desactivaran las barreras hechas de ruido de perlin, y fue la eleccion adecuado porque al ser completamente aleatorio y con valores iguales la dificultad es real y          depende de la habilidad y reflejos que la persona que es el objetivo

- ¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?
    *un Walk en simulacion es la foma en la que dan saltos o pasos las distribuciones el tipo levy flight es un walk en el que hay una pequeña probabiliudad de dar un gran salto.


  #### Parte 2: reflexión sobre tu proceso (Metacognición)

- ¿Cuál fue el concepto más abstracto o difícil de “visualizar” para ti en esta unidad? ¿Qué hiciste para finalmente comprenderlo?
    *El Lévy flight me costomucho tiempo entenderlo y la forma en la que lo logre entender fue preguntando e investigando que era ademas de que lo trate de utilizar en la actividad 8 para saber si en verdad lo habia               entendido bien.

- Describe un momento durante el desarrollo de tu obra final (Actividad 08) en el que un “error” o un resultado inesperado te llevó a una idea creativa interesante.
    *el error que tuve fue que podia pasar aun si tocaba las cuerdas ahi se me ocurrio hacer un sistema de vidas para empezar de nuevo, tambien puse el noise muy agresivo y eso mataba al jugador muy rapido entonces se me        dio la idea de que perlin tuviera un poco de movimiento para que fuera mas complicado
  
- Al combinar diferentes técnicas de aleatoriedad, ¿Cuál fue el mayor desafío? ¿La interacción entre los sistemas, el control de los parámetros, el rendimiento?
    *el mayor reto era combinar diferentes formas aleatorias y que se vieran como una sola pieza y no como cosas separadas
  
- Si tuvieras que empezar la Actividad 08 de nuevo, ¿Qué harías de manera diferente basándote en lo que sabes ahora?
    *lo que haria diferente seria aplicar de diferente manera la inmunidad y tambien el ruido de perlin



### Actividad 10

#### Retroalimentación a Juana Vargas Ossa

En general se aplican muy bien lois conceptos vistos en clase y esta bien estructurado directamente de lo que se pide en la actividad 8 cumple con todos los criterios Solo tengo una observacion breve

En esta parte del codigo:
```javascript
function updateSnake1() {
  let head = snake1[0].copy();
  let target = createVector(mouseX, mouseY);

  let dir = p5.Vector.sub(target, head);
  let maxStep = 6; // Más rápida para esta serpiente
  if (dir.mag() > maxStep) {
    dir.setMag(maxStep);
  }
  snake1[0] = p5.Vector.add(head, dir);

  for (let i = 1; i < len; i++) {
    let prev = snake1[i - 1].copy();

    let angleNoise = noise(prev.x * noiseScale1, prev.y * noiseScale1, t1 + i * 0.1);
    let biasedNoise = pow(angleNoise, 3);
    let angle = map(biasedNoise, 0, 1, -PI, PI);
    let step = p5.Vector.fromAngle(angle).mult(5);
    snake1[i] = p5.Vector.lerp(snake1[i], p5.Vector.add(prev, step), 0.5);
  }
```
la inicializacion de las serpientes depende directamente de el movimiento del mouse si este no se mueve no tiene direccion eso se cambia muy sencillo entonces no me parece que reduzca la nota jeje.

### Actividad 11

#### Feedback

- Continuar: ¿Qué actividad, ejemplo o explicación de esta unidad te resultó más reveladora o útil para tu aprendizaje? ¿Qué deberíamos mantener sí o sí?
     *la actividad de las normales y distribucion uniforme y o uniforme creo que eso da pie a que se hagan muchas cosas con mun poco de imaginación.
- Dejar de hacer: ¿Hubo alguna actividad o concepto que te pareció redundante, confuso o menos útil? ¿Hay algo que eliminarías o cambiarías por completo?
     *siento que toda la unidad fue muy competa y creo que todos los conceptos eran necesarios me gustó. 
- Empezar a hacer: ¿Qué te faltó en esta unidad? ¿Quizás más ejemplos de artistas, más desafíos técnicos, más teoría? ¿Qué idea tienes para hacerla mejor?
     *yo creo que depronto en los ultimos dos conceptos que si eran un poco mas complejos seria mejor tener un video donde lo expliquen mas que solo un documento para leer.
  
- Balance Teoría-Práctica: ¿Cómo sentiste el equilibrio entre analizar los ejemplos del texto guía y ponerte a programar tus propios sketches? Explica tu respuesta.
     *me gusta mucho es muy positivo y siento que entendí muy bien, ese equilibrio me hace sentir que si entendi los temas y me ayuda a saber cuales no entendi del todo y poderlos reforzar.
  
- Comentario Adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad?
     *Fue muy interesante las diferentes formas de aleatoriedad que existen en el arte generativo y todo lo que se puede hacer con base en esto siento que esto se puede aplicar en muchas cosas me gustó mucho esta unidad          porque me hizo imaginarme muchas ideas locas de como usralo.
