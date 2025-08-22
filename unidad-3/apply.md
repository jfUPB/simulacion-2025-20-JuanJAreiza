# Unidad 3


## 🛠 Fase: Apply

1.
### Mi obra se llama: __Digital Mariposa.__

#### Es interactiva con:
##### Mouse:
- __Click izquierdo:__ crear pieza pequeña.
- __Click derecho:__ crear pieza grande).
##### Teclado:
- __Tecla 'Espacio'__ para pausar la obra y apreciarla.
- __Tecla 'R'__ para reiniciar las conexiones hechas.
- __Tecla 'S'__ para tomar pantallazo.

#### ¿Qué usé?
- Usé Random, Perlin, Distribución Gaussiana y LerpColor.

2. ### ¿Cómo lo modelé?
En esta obra me inspiré mucho en las esculturas cinéticas de Alexander Calder, por no decir que intenté hacer un calco digital de su estética, pero siendo totalmente generativo: un montón de partículas que se mueven y se atraen entre sí: esto por medio de dos ciclos constantes, en los cuales es importantisimo "saltarse" (no aplicar fuerza) aquel que tenga el mismo id a la vez en los dos ciclos, porque no puede atraerse a si mismo.

Cada figura tiene la __posibilidad de conectarse__ a otras unas 2 veces en total, permitiendo así que hayan estas __vinculaciones tan destacables en sus obras__, que aunque no tengan equilibrio, se pueden imaginar.

Además __cada pieza cambia de color suavemente usando lerpColor y Perlin__, y algunas salen __más grandes o más chicas gracias a la distribución gaussiana__, lo que da variedad y hace que el movimiento se vea más orgánico. Todo esto con la intención de tener una identidad puramente de Calder, donde __los colores y las formas sean tan variados que destaquen en su impacto visual y su movimiento.__

3. [Enlace a mi Actividad 10](https://editor.p5js.org/JuanJAreiza/sketches/-0WDvF4Xf)
4.
``` js
let bodies = [];
let connections = [];
let colors = [];
let paused = false;
let tNoise = 0;
let G = 10;


function setup() {
  let canvas = createCanvas(500, 500);
  
  colors = [
    color(0, 102, 255),    // Azul
    color(0, 179, 255),    // Otro azul mas claro
    color(255, 128, 0),    // Naranja
    color(255, 221, 51),   // Amarillo
    color(204, 0, 0),      // Rojo
    color(188, 188, 188),  // Blanco
    color(0, 0, 0)         // Negro
  ]
  
  canvas.elt.addEventListener("contextmenu", (e) => e.preventDefault());
}

function draw() {
  if (paused) return;
  background(240);
  tNoise += 0.005;

  // aplico n-bodies
  for (let i = 0; i < bodies.length; i++) {
    for (let j = 0; j < bodies.length; j++) {
      if (i !== j) {
        let force = bodies[j].attract(bodies[i]);
        bodies[i].applyForce(force);
      }
    }
  }

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

    let baseSize = big ? 60 : 30;
    // Aquí apliqué distri. gaussiana (desviación 0.35 y con límites)
    let gaussianFactor = constrain(randomGaussian(1, 0.35), 0.5, 2.0);
    this.size = baseSize * gaussianFactor;

    this.pos = createVector(x, y);
    this.vel = createVector(random(-1, 1), random(-1, 1));
    this.acc = createVector(0, 0);
    this.type = int(random(4)); //
    this.connections = 0;
    this.noiseOffset = random(1000);
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

    // Para no salir del canvas
    if (this.pos.x < this.size/2 || this.pos.x > width - this.size/2) {
      this.vel.x *= -1;
    }
    if (this.pos.y < this.size/2 || this.pos.y > height - this.size/2) {
      this.vel.y *= -1;
    }
  }

  //Aquí apliqué Perlin y lerpColor para el cambio del color
  getColor() {
    let n = noise(tNoise + this.noiseOffset);
    let idx = int(n * colors.length) % colors.length;
    let nextIdx = (idx + 1) % colors.length;
    let amt = (n * colors.length) % 1;
    return lerpColor(colors[idx], colors[nextIdx], amt);
  }


  display() {
    noStroke();
    fill(this.getColor());

    switch (this.type) {
      case 0:
        circle(this.pos.x, this.pos.y, this.size);
        break;
      case 1:
        triangle(
          this.pos.x, this.pos.y - this.size/2,
          this.pos.x - this.size/2, this.pos.y + this.size/2,
          this.pos.x + this.size/2, this.pos.y + this.size/2
        );
        break;
      case 2:
        ellipse(this.pos.x, this.pos.y, this.size, this.size * 0.6);
        break;
      case 3:
        push();
        rectMode(CENTER);
        square(this.pos.x, this.pos.y, this.size);
        pop();
        break;
    }
  }

  canConnect() {
    return this.connections < 2;
  }
}

class Connection {
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
  display() {
    line(this.a.pos.x, this.a.pos.y, this.b.pos.x, this.b.pos.y);
  }
}

function alreadyConnected(a, b) {
  for (let c of connections) {
    if ((c.a === a && c.b === b) || (c.a === b && c.b === a)) return true;
  }
  return false;
}

function mousePressed() {
  if (mouseButton === LEFT) {
    bodies.push(new Body(mouseX, mouseY, random(0.1, 2), false));
  }
  if (mouseButton === RIGHT) {
    bodies.push(new Body(mouseX, mouseY, random(2, 6), true));
  }
}

function keyPressed() {
  if (key === ' ') paused = !paused;
  if (key === 'R' || key === 'r') {
    connections = [];
    for (let b of bodies) b.connections = 0;
  }
  if (key === 'S' || key === 's') saveCanvas('obraUnidad3', 'jpg');
}
```
5. __Captura:__
Comparto dos porque me parecieron muy interesantes.
![obraUnidad3 (2)](https://github.com/user-attachments/assets/2daa4f0e-ab2f-4e50-ae13-b38a47cd9cd0)
![obraUnidad3](https://github.com/user-attachments/assets/ef567305-1667-446a-9a11-2ec1ef6e0b54)

