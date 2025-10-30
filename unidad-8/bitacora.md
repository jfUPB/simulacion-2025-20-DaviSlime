# Evidencias de la unidad 8

## Actividad 1

1. Describe tus observaciones sobre la conexión sonido-imagen en al menos dos de las performances vistas.

Sónar+D CCCB 2020 Music: me parecio incdreible como solo con simples lineas y colores diferentes se puede expresar las emociones de calma e intensidad del piano.

Dimension N: combina muchos estilos diferentes desde la forma de una onda hasta construciones complejas que lo invitan a uno a mantenerse enfocado en como va a surgir los proximos sonidos, bastante interesante.

2. Explica qué elementos te parecieron generativos y por qué crees que cada visualización sería única.

algunos elementos que me parecieron generativos fueron por ejemplo las ondas circulares de la presentacion de Dimension N, donde se creaban aleatoriamente pero como creando una especie de parton al ritmo de la uscioca tambien las lineas formadas cada que se tocaba un instrumento distinto en **Sónar+D CCCB** me parece que es algo unico que solo se va a mostrar una vez ya que como tiene factor de aleatoriedad nunca se va aver la misma presentacion simpre va a cambiar.

3. Comparte tu reflexión sobre la sensación de “liveness”.

la senascion que genera es una sensacion de exclusividad ya que esas mismas visuales solo las van a poder ver una sola vezz ningun concierto va a tomar esas formas iguales y ademas ver esas visuales en tiempo real al igual que la musica en vivo como en los conciertos hace que se sienta una conexion especial de que alguien al mismo tiempo que esta escuchando la cancion esta generando estos cambios.

## Actividad 2

1. La pieza musical elegida (con enlace/archivo si es posible).

    [Imagine Dragons - Whatever It Takes]([https://youtu.be/1ObzXAahwnM?si=bsHvWoLMnNEWw_A3](https://youtu.be/UsuF4jJ4sgA?si=P9r_vIlUd-gPygkx))

Esta canción combina energía, intensidad rítmica y una atmósfera motivacional que se traduce visualmente en un viaje de fuerza y superación. Su estructura con bajos potentes y crescendos marcados la hace ideal para generar una experiencia inmersiva y visualmente dinámica.

2. La descripción de tu concepto visual.

El visualizador está inspirado en la idea de atravesar un túnel de energía al ritmo de la música, simbolizando el proceso de transformación interna que evoca la canción.
El espectador “viaja” a través de un espacio tridimensional lleno de partículas luminosas que se desplazan hacia la cámara, dando la sensación de velocidad, expansión y trascendencia.

El centro del túnel representa el corazón de la energía musical, donde los beats y frecuencias bajas generan pulsaciones y explosiones visuales que responden directamente a la intensidad sonora.
El uso del color dinámico (basado en el espectro HSB) refuerza la emoción de cada momento, creando una sinestesia entre sonido y movimiento.

En resumen, el concepto busca visualizar la fuerza interior que impulsa a seguir adelante, exactamente como transmite la canción “Whatever It Takes”.

3. Los inputs seleccionados y la justificación de por qué los elegiste.

los imputs que yo decidi utilizar son:

os inputs que se implementaron son:

Carga de archivo de audio (input type="file")
→ Permite al usuario seleccionar cualquier canción desde su dispositivo, fomentando la personalización de la experiencia sonora.

Botones WASD
→ Permiten moverse ligeramente dentro del espacio 3D, brindando control y exploración del entorno, simulando la sensación de pilotar a través del túnel.

Slider de sensibilidad
→ Ajusta cuán fuerte reaccionan las partículas y los anillos ante los cambios de frecuencia, permitiendo adaptar la visualización a diferentes estilos de música.

Slider de velocidad
→ Modifica la rapidez con que las partículas y los anillos se desplazan, afectando la percepción de profundidad y dinamismo.

Botón “E” (Explosión visual)
→ Genera un estallido de partículas desde el centro del túnel, sincronizado con el beat o a voluntad del usuario. Representa un clímax energético dentro de la experiencia.

Estos controles permiten que el usuario no solo sea espectador, sino parte activa de la composición visual, ajustando la experiencia según su gusto y ritmo emocional

4. ¿Qué algoritmos o técnicas planeas usar (ej: flow fields, flocking, física, partículas, etc.) y por qué?

El proyecto utiliza una combinación de sistemas de partículas y efectos de profundidad en 3D, optimizados con p5.js y WebGL:

Sistema de partículas:
Cada partícula tiene su propia posición, velocidad y color que varía según la energía del audio. Esto crea la ilusión de materia luminosa que se acerca al espectador.

Anillos concéntricos:
Simulan un túnel tridimensional que se mueve hacia la cámara, reforzando la sensación de avance y continuidad.

Análisis de frecuencia (FFT y Amplitude):
Permite que el movimiento y color de los elementos reaccionen directamente al espectro sonoro, creando una conexión visual-auditiva real.

Explosión procedural:
Se activa mediante el teclado y genera una expansión temporal de las partículas, logrando un efecto de energía liberada desde el centro.

Controles interactivos (WASD y sliders):
Añaden una capa de interacción lúdica, donde el usuario puede modificar parámetros en tiempo real, dando un toque performativo.

5. Tus bocetos y una explicación de cómo los inputs influirán en los visuales.




Archivo de audio (input de canción):
El archivo cargado determina por completo la respuesta visual. El análisis de frecuencias (FFT) extrae datos de bajos, medios y agudos, que influyen en el color, tamaño y velocidad de las partículas. Así, cada canción genera una interpretación visual única.

Slider de sensibilidad:
Controla cuánto responden las partículas y los anillos a la energía del sonido.
→ A mayor sensibilidad, los movimientos son más intensos y los colores cambian con mayor frecuencia.
→ A menor sensibilidad, el movimiento se suaviza, logrando un efecto más atmosférico.

Slider de velocidad:
Ajusta la velocidad de desplazamiento del túnel y de las partículas hacia la cámara.
Esto modifica la sensación de profundidad y la intensidad del viaje visual — valores altos generan una experiencia más energética, mientras que valores bajos la vuelven más relajada.

Botones WASD:
Permiten al usuario desplazarse ligeramente dentro del espacio 3D.
Este control brinda una sensación de exploración y libertad, haciendo que el usuario “vuele” dentro del túnel y sienta que lo atraviesa desde diferentes ángulos.

Botón “E” (explosión):
Provoca un estallido visual de partículas desde el centro, simulando una liberación de energía que reacciona tanto a la música como a la acción del usuario.
Representa un punto de clímax o énfasis emocional dentro de la experiencia, sincronizado con los beats o los momentos más intensos de la canción.
