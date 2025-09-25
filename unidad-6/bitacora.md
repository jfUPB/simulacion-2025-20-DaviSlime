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

2. **Lista los parámetros clave identificados (radio de percepción, pesos de las reglas, maxspeed, maxforce).**

3. **Describe la modificación que realizaste al código y explica detalladamente el efecto que tuvo en el comportamiento colectivo del enjambre (¿Se dispersan? ¿Forman grupos compactos? ¿se mueven caóticamente?). Incluye una captura de pantalla o GIF si ilustra bien el cambio. Muestra el fragmento de código modificado.**


## Actividad 5

### ¿Que hacer?

1. Elige un tema musical que te inspire.

2. Diseña una pieza de arte generativo que utilice el algoritmo de flow fields y/o flocking.

3. Vas a visualizar el tema musical y además vas a “tocar” las visuales, es decir, tu pieza de arte debe ser interactiva y debe permitir la interpretación en tiempo real de las visuales como si fuera un instrumento más que acompaña de manera coherente el tema musical.

### Reporte

1. **Documenta todo el proceso de diseño y creación en tu bitácora, incluyendo bocetos y decisiones de diseño.**


2. **El código fuente completo de tu sketch en p5.js.**


3. **Un enlace a tu sketch en el editor de p5.js.**


4. **Capturas de pantalla mostrando tu pieza en acción.**


## Autoevaluación



