# Unidad 2


## 🛠 Fase: Apply

### Actividad 8:
1. __El hilo rojo:__ De acuerdo a la cultura de Asia Oriental, es un simbolo que conecta a dos personas que están destinadas a estar juntas sin importar el contexto, la situación o los obstaculos. Esta obra intenta representar el pre-encuentro de dos entidades, donde el punto de origen representa una y __el otro es representado por la ubicación o movimiento que se le dé al mouse__.

Este concepto explora el comportamiento colectivo de múltiples entidades que responden dinámicamente a la presencia del mouse en pantalla. Por medio de __atracción y repulsión__, combinado con movimientos inspirados en __caminatas Lévy y el ruido Perlin__, se genera una composición visual en constante movimiento. Además, la __distancia__ que exista __entre la entidad y al mouse__, __cambiará tanto su color (colorLerp), como su grosor.__

2 y 3. Cada entidad tiene su propio vector de posición, velocidad y aceleración, los cuales se actualizan en tiempo real. La aceleración usada resulta de la __combinación de dos fuerzas:__ una basada en la __atracción/repulsión hacia el cursor__ y otra mediante un movimiento __tipo Lévy__, alternable entre random y noise.

4. Controles:
- __Mouse:__ Desplazamiento que cambia color, grosor y desplazamiento/aceleración de cada entidad.
- __F:__ Agregar fondo con alpha reducido.
- __R:__ Cambiar entre atracción y repulsión de las entidades con respecto al mouse.
- __L:__ Cambiar la aceleración/comportamiento (al quitar Lévy de la aceleración) de cada entidad.
- __N:__ Cambiar entre Noise y Random para el comportamiento de Lévy.

5. Código:
``` js
let entidades = [];
let numEntidades = 100;
let morado, rojo;
let agregarFondo = false;
let repulsion = false;
let usarLevy = true;
let usarNoise = false;

function setup() {
  createCanvas(800, 600);
  background(255);
  morado = color(128, 0, 128);
  rojo = color(255, 100, 100);
  strokeWeight(2);

  
  for (let i = 0; i < numEntidades; i++) {
    entidades.push(new Entidad());
  }
}

function draw() {
  
  if (agregarFondo) {
    background(255,90)
    agregarFondo = false;
  }
  
  for (let entidad of entidades) {
    entidad.actualizar();
    entidad.dibujar();
  }
}

function keyPressed() {
  // Agrega un fondo con alpha reducido al presionar:
  if (key === 'f' || key === 'F') {
    agregarFondo = !agregarFondo;
  }
  // Provoca repulsión en las entidades al presionar:
  if (key === 'r' || key === 'R') {
    repulsion = !repulsion;
  }
  //Cambiar la aceleración al presionar:
  if (key === 'l' || key === 'L') {
    usarLevy = !usarLevy;
  }
  //Cambiar entre noise y random del Lévy al presionar:
  if (key === 'n' || key === 'N') {
    usarNoise = !usarNoise;
  }
}


class Entidad {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = p5.Vector.random2D().mult(random(0.5, 2));
    this.acc = createVector(0, 0);
    this.offset = random(TWO_PI);
    
  }

  actualizar() {
    let mouse = createVector(mouseX, mouseY);
    let dir = p5.Vector.sub(mouse, this.pos);
    let distance = dir.mag();
    dir.normalize();
    
    let wave = sin(frameCount * 0.05 + this.offset) * 0.5;
    dir.rotate(wave);

    // Atracción hacia el mouse y dispersión si aplica
    let fuerza = repulsion ? -0.05 : 0.05;
    let attraction = dir.mult(fuerza);

    // Lévy
    let levy = createVector(0, 0);
if (usarLevy) {
  let theta, r;
  if (usarNoise) {
    theta = noise(this.offset + frameCount * 0.01) * TWO_PI;
    r = pow(noise(this.offset + 100 + frameCount * 0.01), -1.5);
  } else {
    theta = random(TWO_PI);
    r = pow(random(1), -1.5);
  }
  levy = createVector(cos(theta), sin(theta)).mult(r * 0.05);
}


    this.acc = p5.Vector.add(attraction, levy);
    this.vel.add(this.acc);
    this.vel.limit(2);
    this.pos.add(this.vel);
    
    this.pos.x = constrain(this.pos.x, 0, width);
    this.pos.y = constrain(this.pos.y, 0, height);
  }

  dibujar() {
    let mouse = createVector(mouseX, mouseY);
    let distance = p5.Vector.dist(mouse, this.pos);

    let maxDist = dist(0, 0, width, height);
    let t = constrain(map(distance, 0, maxDist, 1, 0), 0, 1);
    let col = lerpColor(morado, rojo, t);
    
    let grosor = map(distance, 0, maxDist, 4, 0.5);
    strokeWeight(grosor);
    stroke(col);
    point(this.pos.x, this.pos.y);
  }
}

```
6. Aquí está el [enlace a mi código en p5*](https://editor.p5js.org/JuanJAreiza/sketches/8Zne-eGUw)


7. Captura de pantalla:
<img width="2270" height="957" alt="image" src="https://github.com/user-attachments/assets/c3c5e415-09c5-4968-8624-bd2546447e3d" />


