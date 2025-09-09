# Evidencias de la unidad 5

## Actividad 2


1- El ejemplo 4.2: an Array of Particles.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

**Creación:**
Se crean nuevas instancias de ``Particle`` en cada frame con ``addParticle()`` y se agregan a un ``ArrayList<Particle>``.

**Desaparición:**
Cada partícula tiene una propiedad ``lifespan`` que decrece con el tiempo.
Cuando el `lifespan`` llega a 0, se considera "muerta".

**Gestión de memoria:**
En el método ``run()``, se hace un loop por el ArrayList y se eliminan las partículas muertas con ``particles.remove(i)``.
Esto evita que se acumulen en memoria.

2- El ejemplo 4.4: a System of Systems.

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

3- El ejemplo 4.5: a Particle System with Inheritance and Polymorphism.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?


4- El ejemplo 4.6: a Particle System with Forces.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?


5- El ejemplo 4.7: a Particle System with a Repeller.

 ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

