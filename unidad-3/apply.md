# Unidad 3


## 🛠 Fase: Apply

//Cambiar por figuras 2D primitivas, agregar otro algoritmo de la Unidad 1

1.
### Mi obra se llama: ______________.

#### Es interactiva con:
##### Mouse:
- __Click izquierdo:__ crear pieza pequeña.
- __Click derecho:__ crear pieza grande).
##### Teclado:
- __Tecla 'Espacio'__ para pausar la obra y apreciarla.
- __Tecla 'R'__ para reiniciar las conexiones hechas.
- __Tecla 'S'__ para tomar pantallazo.

#### ¿Qué usé?
- Usé Perlin y ______.

2. ### ¿Cómo lo modelé?


3. [Enlace a mi Actividad 10](https://editor.p5js.org/JuanJAreiza/sketches/-0WDvF4Xf)
4.
``` js
   let bodies = [];
let connections = [];
let paused = false;
let tNoise = 0;
let G = 10;

const COLORS = [
  [0, 119, 255],   // azul
  [255, 119, 0],   // naranja
  [255, 230, 0],   // amarillo
  [255, 0, 0]      // rojo
];

function setup() {
  createCanvas(500, 500);
}

function draw() {
  if (paused) return;
  background(240);
  tNoise += 0.01;

  // aplicar fuerzas n-cuerpos entre cada par
  for (let i = 0; i < bodies.length; i++) {
    for (let j = 0; j < bodies.length; j++) {
      if (i !== j) {
        let force = bodies[j].attract(bodies[i]);
        bodies[i].applyForce(force);
      }
    }
  }

  // actualizar cuerpos
  for (let b of bodies) {
    b.update();
    b.display();
  }

  // crear conexiones nuevas
  for (let i = 0; i < bodies.length; i++) {
    for (let j = i + 1; j < bodies.length; j++) {
      let a = bodies[i];
      let b = bodies[j];
      if (!alreadyConnected(a, b) && a.canConnect() && b.canConnect()) {
        if (dist(a.pos.x, a.pos.y, b.pos.x, b.pos.y) <= (a.size + b.size) / 2) {
          connections.push(new Connection(a, b));
          a.connections++;
          b.connections++;
        }
      }
    }
  }

  // mostrar conexiones
  stroke(0);
  strokeWeight(2);
  for (let c of connections) c.display();
}

class Body {
  constructor(x, y, m, big) {
    this.mass = m;
    this.size = big ? 60 : 30;
    this.pos = createVector(x, y);
    this.vel = createVector(random(-1,1), random(-1,1));
    this.acc = createVector(0, 0);
    this.type = int(random(4)); // forma
    this.connections = 0;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acc.add(f);
  }

  attract(other) {
    let force = p5.Vector.sub(this.pos, other.pos);
    let distance = force.mag();
    distance = constrain(distance, 5, 100);
    let strength = (G * this.mass * other.mass) / (distance * distance);
    force.setMag(strength);
    return force;
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);

    // Para que no salga del Canvas
    if (this.pos.x < this.size/2 || this.pos.x > width - this.size/2) {
      this.vel.x *= -1;
    }
    if (this.pos.y < this.size/2 || this.pos.y > height - this.size/2) {
      this.vel.y *= -1;
    }
  }

  getColor() {
    let n = noise(tNoise + this.pos.x*0.005, this.pos.y*0.005);
    let idx = floor(map(n, 0, 1, 0, COLORS.length));
    return COLORS[idx];
  }

  display() {
    noStroke();
    let col = this.getColor();
    fill(col[0], col[1], col[2]);

    switch(this.type){
      case 0:
        ellipse(this.pos.x, this.pos.y, this.size);
        break;
      case 1:
        rectMode(CENTER);
        square(this.pos.x, this.pos.y, this.size);
        break;
      case 2:
        rectMode(CENTER);
        rect(this.pos.x, this.pos.y, this.size, this.size*0.6);
        break;
      case 3:
        push();
        translate(this.pos.x, this.pos.y);
        beginShape();
        vertex(-this.size/2, this.size/2);
        vertex(0, -this.size/2);
        vertex(this.size/2, this.size/2);
        endShape(CLOSE);
        pop();
        break;
    }
  }

  canConnect(){
    return this.connections < 2;
  }
}

class Connection {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
  display(){
    line(this.a.pos.x, this.a.pos.y, this.b.pos.x, this.b.pos.y);
  }
}

function alreadyConnected(a, b){
  for(let c of connections){
    if((c.a===a && c.b===b)||(c.a===b && c.b===a)) return true;
  }
  return false;
}

function mousePressed() {
  if (mouseButton === LEFT) {
    bodies.push(new Body(mouseX, mouseY, random(0.1, 2), false));
  }
  if (mouseButton === RIGHT) {
    bodies.push(new Body(mouseX, mouseY, random(2, 6), true));
    return false; // evitar menú contextual
  }
}

function keyPressed(){
  if(key === ' ') paused = !paused;
  if(key === 'R' || key === 'r'){
    connections = [];
    for(let b of bodies) b.connections = 0;
  }
  if(key === 'S' || key === 's') saveCanvas('obra-nbodies', 'png');
}
```
5. __Captura:__
