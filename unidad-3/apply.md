# Unidad 3


## 🛠 Fase: Apply

### Actividad 10

### Explicación del código de simulación n-cuerpos

#### 1. Modelado del problema de los n-cuerpos

El problema de los n-cuerpos consiste en simular el movimiento de **n partículas** que se atraen mutuamente por una fuerza, generalmente gravitacional. En este código:

- Cada partícula es un objeto con posición, velocidad, aceleración y masa.
- Las partículas se atraen **entre sí** calculando la fuerza gravitacional entre pares, usando la ley de gravitación universal simplificada:

<img width="122" height="46" alt="image" src="https://github.com/user-attachments/assets/5c6bdb16-c8b6-46a2-997a-4f96c24a44da" />


- Además, todas las partículas sienten una **atracción hacia el mouse**, que actúa como un cuerpo de masa grande fijo en la posición del cursor, con una constante gravitacional mayor (`mouseG`).
- Cada cuadro (`draw`) se calcula la suma de fuerzas sobre cada partícula (atracción entre partículas + atracción al mouse), actualizando aceleración, velocidad y posición.
- Se usa un método simple de integración:  
  - \(v = v + a\)  
  - \(x = x + v\)  
  - y luego se resetea la aceleración.

Este modelo representa una simulación simplificada del sistema n-cuerpos, donde las partículas interactúan mediante fuerzas mutuas, y el mouse agrega un cuerpo extra externo que altera el sistema.

---

#### 2. Algoritmos usados (además de `random()`)

| Algoritmo                      | Uso en el código                                             |
|-------------------------------|--------------------------------------------------------------|
| **Vectores (pos, vel, acc)**  | Para modelar posición, velocidad y aceleración de partículas, y operaciones vectoriales (suma, resta, magnitud). Se usa `p5.Vector`. |
| **Aplicación de fuerzas**      | Basado en física: \(F = ma\), la fuerza se convierte en aceleración dividiendo por la masa. |
| **Límites (constrain)**        | Para evitar que la fuerza sea infinita o muy grande cuando las partículas están muy cerca (distancia mínima). |
| **Iteración doble**            | Para calcular fuerza entre todas las partículas (doble loop) — típica en simulaciones n-cuerpos. |
| **Mapeo proporcional**         | La fuerza gravitacional depende inversamente al cuadrado de la distancia (\(1/d^2\)). |

---

#### 3. Tabla de controles (teclas)

| Tecla        | Acción                                                       |
|--------------|--------------------------------------------------------------|
| **a**        | Cambia el color de **todas** las partículas a un nuevo color aleatorio (único color para todas). |
| **s**        | Aumenta la fuerza gravitacional tanto entre partículas (`G`) como hacia el mouse (`mouseG`). |
| **d**        | Disminuye la fuerza gravitacional entre partículas y hacia el mouse (sin pasar de 0). |
| **barra espaciadora (space)** | Reinicia toda la simulación: reposiciona partículas, resetea fuerzas y colores. |

---

#### 4. Relacion con Alexander Calder

| Elemento                               | Obra generativa (p5.js)                                          | Obra de Calder                                                  |
| -------------------------------------- | ---------------------------------------------------------------- | --------------------------------------------------------------- |
| **Movimiento constante**               | Las partículas están en movimiento continuo.                     | Las piezas móviles se balancean y giran constantemente.         |
| **Interacción con fuerzas invisibles** | Atracción gravitacional entre partículas y hacia el mouse.       | Influencia del viento, gravedad y equilibrio físico.            |
| **Interdependencia de elementos**      | Las partículas se afectan mutuamente, como un sistema n-cuerpos. | Cada parte del móvil afecta a las demás a través del balanceo.  |
| **Sensibilidad al entorno**            | El usuario modifica fuerzas con teclas y el mouse.               | El aire o el tacto pueden alterar el movimiento de los móviles. |
| **Estética del caos y el equilibrio**  | Movimiento aparentemente caótico pero armónico y fluido.         | Composición visual que parece aleatoria pero está equilibrada.  |

---

### Enlace a la simulación

https://editor.p5js.org/DaviSlime/sketches/isYaFj32q

### Código

```javascript
let particles = [];
let G = 0.4;       // Constante gravitacional para interacción entre partículas
let mouseG = 1.5;  // Constante gravitacional para atracción al mouse (más fuerte)
let numParticles = 20;
let currentColor;

function setup() {
  createCanvas(windowWidth, windowHeight);
  initParticles();
  background(0);
}

function draw() {
  noStroke();
  fill(0, 20);
  rect(0, 0, width, height);

  let mousePos = createVector(mouseX, mouseY);

  // Dibuja líneas ("cuerdas") entre partículas
  stroke(currentColor);
  strokeWeight(0.5);
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      line(particles[i].pos.x, particles[i].pos.y, particles[j].pos.x, particles[j].pos.y);
    }
  }
  noStroke();

  for (let p of particles) {
    p.attractedToMouse(mousePos);
    for (let other of particles) {
      if (p !== other) {
        p.attractedToParticle(other);
      }
    }
    p.update();
    p.checkEdges();
    p.show();
  }
}

function keyPressed() {
  if (key === 'a') {
    currentColor = color(random(255), random(255), random(255));
    for (let p of particles) {
      p.color = currentColor;
    }
  } else if (key === 's') {
    mouseG += 0.2;
    G += 0.1;
  } else if (key === 'd') {
    mouseG = max(0, mouseG - 0.2);
    G = max(0, G - 0.1);
  } else if (key === ' ') { // Barra espaciadora
    initParticles();
    background(0);
  }
}

function initParticles() {
  currentColor = color(255, 150, 0); // Color inicial (naranja)
  particles = [];
  for (let i = 0; i < numParticles; i++) {
    particles.push(new Particle(currentColor));
  }
  G = 0.4;
  mouseG = 1.5;
}

class Particle {
  constructor(col) {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(0, 0);
    this.acc = createVector();
    this.mass = random(2, 5);
    this.color = col;
  }

  attractedToMouse(target) {
    let force = p5.Vector.sub(target, this.pos);
    let d = constrain(force.mag(), 5, 50);
    let strength = (mouseG * this.mass) / (d * d);
    force.setMag(strength);
    this.applyForce(force);
  }

  attractedToParticle(other) {
    let force = p5.Vector.sub(other.pos, this.pos);
    let d = constrain(force.mag(), 5, 100);
    let strength = (G * this.mass * other.mass) / (d * d);
    force.setMag(strength);
    this.applyForce(force);
  }

  applyForce(f) {
    let fCopy = f.copy().div(this.mass);
    this.acc.add(fCopy);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }
  
  // Rebotar en los bordes
  checkEdges() {
    if (this.pos.x < 0) {
      this.pos.x = 0;
      this.vel.x *= -1;
    } else if (this.pos.x > width) {
      this.pos.x = width;
      this.vel.x *= -1;
    }
    if (this.pos.y < 0) {
      this.pos.y = 0;
      this.vel.y *= -1;
    } else if (this.pos.y > height) {
      this.pos.y = height;
      this.vel.y *= -1;
    }
  }

  show() {
    fill(this.color);
    ellipse(this.pos.x, this.pos.y, this.mass * 2);
  }
}



```

### Imagen representativa

<img width="942" height="806" alt="image" src="https://github.com/user-attachments/assets/5ad49750-8cbd-45db-8511-03eadd1095b6" />


