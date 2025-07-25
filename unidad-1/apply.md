# Unidad 1

## 🛠 Fase: Apply

Lévy Flight, Distribución Gaussiana y Perlin. Se puede usar mouse, teclado.

### Concepto:
Esta obra simula pinceladas que se mueven solas desde un mismo origen, como si tuvieran vida propia.
Algunas se desplazan con pasos suaves usando ruido Perlin, mientras que otras siguen trayectorias impredecibles con Lévy Flight, generando una relación entre lo fluido y lo caótico.
Los tamaños varían siguiendo una distribución gaussiana, donde la mayoría son similares, pero algunas pinceladas rompen con la norma y se destacan.

Además, el usuario puede intervenir el lienzo:

- Al presionar "r", cambia la paleta de colores.

- Al presionar "c", limpia para una nueva composición.

Así, la obra no solo se genera sola, sino que también hace al espectador parte del proceso, convirtiéndose en una experiencia viva, abierta y en constante generación.

### Código:
```
let walkers = [];
let usePerlin = false;
let t = 0; // Tiempo para el Perlin

function setup() {
  createCanvas(640, 240);
  
  walkers.push(new Walker(color(255, 0, 0, 50), "levy"));
  walkers.push(new Walker(color(0, 255, 0, 50), "levy"));
  
  walkers.push(new Walker(color(0, 0, 255, 50), "perlin"));
  walkers.push(new Walker(color(255, 165, 0, 50), "perlin")); //naranja
  walkers.push(new Walker(color(128, 0, 128, 50), "perlin")); //morado
  
  background(255);
}

function draw() {
  for (let w of walkers) {
    w.step();
    w.show();
  }

  t += 0.01;
}

function keyPressed() {
  if (key === 'c') {
    background(255); // Limpia el lienzo
  }
  if (key === 'r') {
    // Cambia color por aletorios
    for (let w of walkers) {
      w.c = color(random(255), random(255), random(255), 50);
    }
  }
}

class Walker {
  constructor(c, mode) {
    this.x = width / 2;
    this.y = height / 2;
    this.c = c;
    this.mode = mode; // levy o perlin
    this.tx = random(1000); // Tiempo Perlin x
    this.ty = random(2000); // Tiempo Perlin y
  }

  show() {
    noStroke();
    
    // Distribución gaussiana para el tamaño
    let size = constrain(randomGaussian(20, 5), 5, 50);
    
    fill(this.c);
    circle(this.x, this.y, size);
  }

  step() {
    let dx, dy;

    if (this.mode === "levy") {
      let stepSize = random(1) < 0.03 ? random(50, 150) : random(1, 5);
      let angle = random(TWO_PI);
      dx = cos(angle) * stepSize;
      dy = sin(angle) * stepSize;
    } else if (this.mode === "perlin") {
      dx = map(noise(this.tx), 0, 1, -2, 2);
      dy = map(noise(this.ty), 0, 1, -2, 2);
      this.tx += 0.01;
      this.ty += 0.01;
    }

    this.x += dx;
    this.y += dy;

    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }
}

```

### Enlace:
[Pinceladas vivas] (https://editor.p5js.org/JuanJAreiza/sketches/1BesSufHm)

### Captura de pantalla:
<img width="2080" height="1024" alt="image" src="https://github.com/user-attachments/assets/04a618b4-5a4d-48d9-b139-13cbed731cd7" />


