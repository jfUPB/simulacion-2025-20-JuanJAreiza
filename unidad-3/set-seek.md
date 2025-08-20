# Unidad 3

## 🔎 Fase: Set + Seek

1. ¿Cómo modelé cada fuerza?
- __Fricción:__ Agarré la velocidad de cada partícula, le saqué una copia, la normalicé (para quedarme solo con la dirección) y la multipliqué por un número negativo (para que apunte al lado contrario). Ese número negativo también se multiplica por un coeficiente de fricción que cambia según qué tan arriba o abajo esté la partícula (si está abajo, hay más fricción).

- __Resistencia del aire y de fluidos:__ Le puse una zona _(la mitad inferior del canvas)_ que simula un “líquido”. Si la partícula entra ahí, le aplico una fuerza en contra de su movimiento. Esa fuerza es proporcional al cuadrado de su velocidad _(en este caso "speed * speed")_, siguiendo la fórmula dada del drag. La fuerza se calcula copiando su velocidad, normalizándola _(dirección del movimiento)_, multiplicándola por -1 _(para que vaya al revés)_ y por un coeficiente dragC que en este caso cambia con la posición del mouse en el eje X.

- __Atracción gravitacional:__ Basandome directamente en el ejemplo de _Nature of Code_, creé un objeto Attractor con masa. Luego calculo un vector que va desde el attractor hasta el mover _(p5.Vector.sub)_. Miro la distancia entre ambos y la restrinjo con un constrain() para que no se vuelva loca la fuerza.
Ese valor se lo pongo como magnitud al vector dirección y se lo aplico al mover. Si hay muchos attractors, se suman todas las fuerzas.

2. ¿Cómo se relaciona con la obra?
- __Fricción:__ La obra es sobre un material que cambia su desplazamiento dependiendo de la superficie: arriba es rugoso y lento, abajo es jabonoso y amplío. Visualmente se ve como un degradado. Se puede pintar sobre el lienzo y __varía dependiendo de la posición en y de cada partícula generada__.

- __Resistencia del aire y de fluidos:__ La obra es sobre __partículas que se generán por el usuario__ libremente en el aire (es decir, la parte superior del canvas), __arrastrando el mouse mientras se presiona click__,  pero al entrar en una piscina de miel/agua se empiezan a frenar y hundir más lentamente, todo eso dependiendo de la posición del usuario de izquierda a derecha.

- __Atracción gravitacional:__ La obra consiste en tener varios imanes en el espacio, donde el Mover se desplaza de forma variada entre ellos. Con __click el usuario puede “diseñar campos gravitatorios”, es decir, poner más attractos en el canvas__ y ver cómo reaccionan los objetos.

3. Enlaces:
[Enlace a Fricción](https://editor.p5js.org/JuanJAreiza/sketches/P49ZoLwCY)
[Enlace a Resistencia del aire y de fluidos](https://editor.p5js.org/JuanJAreiza/sketches/xm651UCtV)
[Enlace a Atracción gravitacional](https://editor.p5js.org/JuanJAreiza/sketches/oAdOVhrBs)

4. Códigos:
- __Fricción:__
```
let particles = [];

function setup() {
  createCanvas(500, 500);
}

function draw() {
  // Fondo con zonas de diferente fricción, uso map
  for (let y = 0; y < height; y++) {
    let backgroundBrightness = map(y, 0, height, 255, 20); // más oscuro abajo (20)
    stroke(backgroundBrightness);
    line(0, y, width, y);
  }

  // Actualizar y mostrar partículas
  for (let particle of particles) {
    particle.actualizar();
    particle.dibujar();
  }
}

function mouseDragged() {
  particles.push(new Particle(mouseX, mouseY));
}

function keyPressed() {
  // Para guardar captura
  if (key === "s" || key === "S") {
    saveCanvas("myCanvas", "png");
  }
}

// Clase de partícula
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 1));
  }

  actualizar() {
    // Calcular "brillo" y fricción basado en la posición y
    let brightness = map(this.position.y, 0, height, 1, 0.3); // menos fricción arriba (1) y mas abajo (0.3)
    let friction = this.velocity.copy();
    friction.normalize();
    friction.mult(-0.03 * brightness);
    this.velocity.add(friction);

    // Actualizar posición
    this.position.add(this.velocity);
  }

  dibujar() {
    fill(40, 150, 250, 150);
    ellipse(this.position.x, this.position.y, 12);
  }
}
```
- __Resistencia del aire y de fluidos:__
```
let particles = [];
let dragC = 0.1;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(245);

  // Zona "fluida"
  fill(150, 180, 255, 150);
  rect(0, height / 2, width, height / 2);

  // Coeficiente de arrastre varía con el mouse
  dragC = map(mouseX, 0, width, 0.01, 0.08);

  for (let particle of particles) {
    particle.actualizar();
    particle.dibujar();
  }
}

function mouseDragged() {
  particles.push(new Particle(mouseX, mouseY));
}

function keyPressed() {
  // Para guardar captura
  if (key === "s" || key === "S") {
    saveCanvas("myCanvas", "png");
  }
}

// Clase Partícula
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 1));
    this.acceleration = createVector(0, 0);
    this.size = 10;
  }

  actualizar() {
    // Gravedad
    this.acceleration.add(createVector(0, 0.2));

    // Aplicar arrastre si está en la zona fluida
    if (this.position.y > height / 2) {
      let drag = this.velocity.copy();
      let speed = drag.mag();
      let dragMagnitude = dragC * speed * speed;

      drag.normalize();
      drag.mult(-dragMagnitude);
      this.acceleration.add(drag);
    }

    // Motion 101 :D
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); //Por 0 para reiniciar el vector
  }

  dibujar() {
    fill(40, 150, 250, 150);
    circle(this.position.x, this.position.y, this.size);
  }
}

```

- __Atracción gravitacional:__
```
let particles = [];
let dragC = 0.1;

function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(245);

  // Zona "fluida"
  fill(150, 180, 255, 150);
  rect(0, height / 2, width, height / 2);

  // Coeficiente de arrastre varía con el mouse
  dragC = map(mouseX, 0, width, 0.01, 0.08);

  for (let particle of particles) {
    particle.actualizar();
    particle.dibujar();
  }
}

function mouseDragged() {
  particles.push(new Particle(mouseX, mouseY));
}

function keyPressed() {
  // Para guardar captura
  if (key === "s" || key === "S") {
    saveCanvas("myCanvas", "png");
  }
}

// Clase Partícula
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 1));
    this.acceleration = createVector(0, 0);
    this.size = 10;
  }

  actualizar() {
    // Gravedad
    this.acceleration.add(createVector(0, 0.2));

    // Aplicar arrastre si está en la zona fluida
    if (this.position.y > height / 2) {
      let drag = this.velocity.copy();
      let speed = drag.mag();
      let dragMagnitude = dragC * speed * speed;

      drag.normalize();
      drag.mult(-dragMagnitude);
      this.acceleration.add(drag);
    }

    // Motion 101 :D
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); //Por 0 para reiniciar el vector
  }

  dibujar() {
    fill(40, 150, 250, 150);
    circle(this.position.x, this.position.y, this.size);
  }
}

class Attractor {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.mass = 20;
  }

  attract(mover) {
    let force = p5.Vector.sub(this.position, mover.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 25);
    let strength = (G * this.mass * mover.mass) / (distance * distance);
    force.setMag(strength);
    return force;
  }

  show() {
    stroke(0);
    strokeWeight(1);
    fill(40, 150, 250, 150);
    circle(this.position.x, this.position.y, this.mass * 2);
  }
}

class Mover {
  constructor(x, y, mass) {
    this.mass = mass;
    this.radius = mass * 8;
    this.position = createVector(x, y);
    this.velocity = createVector(1, 0);
    this.acceleration = createVector(0, 0);
  }
  
  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    noStroke();
    fill(40, 150, 250, 150);
    circle(this.position.x, this.position.y, this.radius * 2);
  }
}
```


6. Capturas:
- __Fricción:__ <img width="1000" height="1000" alt="myCanvas (2)" src="https://github.com/user-attachments/assets/ff94f797-b8ed-4036-a1e4-11fa1bf33a20" />

- __Resistencia del aire y de fluidos:__ <img width="1200" height="800" alt="myCanvas (3)" src="https://github.com/user-attachments/assets/c385d798-7177-4ade-a4a2-375c8ed17f00" />

- __Atracción gravitacional:__ <img width="1000" height="1000" alt="myCanvas (1)" src="https://github.com/user-attachments/assets/ebb3fe68-6eb6-4514-ac3e-397c9bd79970" />

