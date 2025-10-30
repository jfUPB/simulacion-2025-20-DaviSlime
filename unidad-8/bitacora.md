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

<img width="1480" height="1920" alt="boceto final" src="https://github.com/user-attachments/assets/17f73fd3-5c4d-4994-b9ab-b0e2c15736b0" />



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



## Actividad 3

1. El código fuente completo de tu sketch en p5.js.

**Index:**

```js
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Túnel Musical Interactivo - Imagine Dragons</title>
  <style>
    html,body {
      margin:0; padding:0; height:100%;
      background:#080814; color:#ddd;
      font-family: Inter, Roboto, sans-serif;
      overflow:hidden;
    }
    #ui {
      position: fixed; top: 12px; left: 12px; z-index: 20;
      background: rgba(0,0,0,0.35);
      padding:10px; border-radius:8px;
      backdrop-filter: blur(6px);
    }
    #ui label { font-size:13px; display:block; margin-bottom:6px; color:#f1f1f7; }
    #ui input[type="file"] { display:block; margin-bottom:8px; }
    #ui button, #ui input[type=range] {
      margin-top:4px;
    }
    #ui button {
      margin-right:6px; padding:6px 10px;
      border-radius:6px; border:none; cursor:pointer;
      background:#3b82f6; color:white; font-weight:600;
    }
    .sliderRow {
      display:flex; align-items:center; justify-content:space-between;
      gap:6px; margin-top:6px;
    }
    .sliderRow label { flex:1; font-size:12px; color:#cde; }
    .sliderRow input { flex:2; }
  </style>
</head>
<body>
  <div id="ui">
    <label>Cargar canción (mp3/ogg):</label>
    <input id="fileinput" type="file" accept="audio/*" />
    <button id="playBtn">▶ Play / Pausa</button>

    <div class="sliderRow">
      <label>🎚 Sensibilidad</label>
      <input id="sensitivitySlider" type="range" min="1" max="10" step="0.1" value="5" />
    </div>
    <div class="sliderRow">
      <label>⚡ Velocidad</label>
      <input id="speedSlider" type="range" min="1" max="15" step="0.1" value="8" />
    </div>
    <p style="font-size:12px; color:#9be7ff; margin-top:6px;">
      Presiona <b>E</b> 💥 para generar una explosión de partículas
    </p>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/p5.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/addons/p5.sound.min.js"></script>
  <script src="sketch.js"></script>
</body>
</html>

```

**Sketch:**

```js
let song, fft, amp;
let isPlaying = false;
let stars = [];
let rings = [];
let energy = 0;
let baseHue = 200;

let speedMult = 8;
let energyMult = 5;
let explosion = 0;
let explosionColorShift = 0;

function setup() {
  createCanvas(windowWidth, windowHeight, WEBGL);
  colorMode(HSB, 360, 100, 100);
  noStroke();

  // Crear partículas del túnel
  for (let i = 0; i < 350; i++) {
    stars.push({
      x: random(-width, width),
      y: random(-height, height),
      z: random(-4000, 0)
    });
  }

  // Crear anillos
  for (let i = 0; i < 10; i++) {
    rings.push({
      z: map(i, 0, 10, -4000, 0),
      r: 500 + i * 150
    });
  }

  const fileInput = document.getElementById("fileinput");
  const playBtn = document.getElementById("playBtn");
  const sensSlider = document.getElementById("sensitivitySlider");
  const speedSlider = document.getElementById("speedSlider");

  fileInput.addEventListener("change", handleFile);
  playBtn.addEventListener("click", togglePlay);

  sensSlider.addEventListener("input", () => (energyMult = sensSlider.value));
  speedSlider.addEventListener("input", () => (speedMult = speedSlider.value));
}

function handleFile(event) {
  const file = event.target.files[0];
  if (!file) return;

  if (song) {
    song.stop();
    song.disconnect();
  }

  song = loadSound(URL.createObjectURL(file), () => {
    userStartAudio();
    fft = new p5.FFT(0.8, 64);
    amp = new p5.Amplitude();
    song.play();
    isPlaying = true;
  });
}

function togglePlay() {
  if (!song) return;
  userStartAudio();
  if (song.isPlaying()) {
    song.pause();
    isPlaying = false;
  } else {
    song.play();
    isPlaying = true;
  }
}

function keyPressed() {
  // Presionar "E" → Explosión de partículas 💥
  if (key === "e" || key === "E") {
    explosion = 5; // intensidad del impulso
    explosionColorShift = 180; // cambio de color temporal
  }
}

function draw() {
  background(0, 0, 5);

  if (!song || !song.isPlaying()) {
    fill(255);
    textAlign(CENTER, CENTER);
    textSize(16);
    text("Selecciona una canción para iniciar 🎵", 0, 0);
    return;
  }

  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass") / 255;
  energy = fft.getEnergy("mid") / 255;
  let level = amp.getLevel();

  translate(0, 0, -800);

  // 🔹 Dibujar anillos del túnel
  for (let r of rings) {
    push();
    translate(0, 0, r.z);
    noFill();

    let hueShift = (baseHue + explosionColorShift + r.z * 0.02) % 360;
    stroke(hueShift, 80, 100);
    strokeWeight(1.5);
    ellipse(0, 0, r.r + bass * 120, (r.r + bass * 120) * 0.6);
    pop();

    r.z += speedMult * (0.5 + energy * 0.8 + explosion * 0.3);
    if (r.z > 200) r.z = -4000;
  }

  // 🔹 Dibujar partículas que vienen hacia la cámara
  for (let s of stars) {
    s.z += speedMult * (1 + energy * energyMult * 0.05 + explosion * 0.8);
    if (s.z > 100) {
      s.z = -4000;
      s.x = random(-width, width);
      s.y = random(-height, height);
    }

    let sx = map(s.x / s.z, 0, 1, 0, width);
    let sy = map(s.y / s.z, 0, 1, 0, height);
    let r = map(s.z, -4000, 100, 0.5, 6);
    fill((baseHue + explosionColorShift + s.z * 0.03) % 360, 90, 100);
    ellipse(sx - width / 2, sy - height / 2, r * (1 + energy * 2));
  }

  // 🔹 Esfera central pulsante
  push();
  let pulse = map(level, 0, 0.3, 40, 120, true);
  fill((baseHue + explosionColorShift + 100 + energy * 80) % 360, 100, 100);
  sphere(pulse, 24, 16);
  pop();

  // 🔹 Suavizar efectos
  explosion *= 0.9; // disipa velocidad
  explosionColorShift *= 0.85; // el color vuelve al original

  baseHue = (baseHue + 0.2 + energy * 0.5) % 360;
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

```

2. Un enlace a tu sketch en el editor de p5.js.

https://editor.p5js.org/DaviSlime/sketches/O2r94jZJX

3. Capturas de pantalla mostrando tu pieza en acción.

<img width="1444" height="771" alt="image" src="https://github.com/user-attachments/assets/de0000f8-898b-4072-b443-d3aa95fc5ddf" />





# AUTOEVALUACION

5 porque complete todas las asignaciones
