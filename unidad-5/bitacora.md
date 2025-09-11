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

