# Evidencias de la unidad 5

### Actividad 02.

## Parte 1.
#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

>1. En este primer caso, se instancia un arreglo que contendrá todas las particulas que se generen. Luego en el draw() se agrega una nueva partícula en el centro superior de la pantalla. Dentro de cada partícula hay un valor "lifespan" que representa como una longevidad de vida, la cual se va reduciendo númericamente y visualmente se representa como que pierde su transparencia al dibujarse. Cuando el "lifespan" baja de 0, el método isDead() devuelve verdadero. Dentro del mismo draw() se comprueba por medio de un "for inverso" -es decir, que hace su recorrido del index restando en vez de sumar, para evitar saltarse comprobaciones de cada partícula- si la partícula está "muerta" y en caso de que sí, es eliminada con splice() del arreglo. Al ya no estar presente en el espacio ni en el arreglo, la memoria se libera automáticamente para dar espacio a una nueva partícula.

>2. Para este caso, la generación de las partículas se hacen por medio de emisores que el usuario crea dando click en cualquier punto del Canvas. Este es un arreglo de "emitters" que los va guardando a la par que son creados. Cada emisor tiene su propio arreglo interno donde guarda las partículas generadas -y posteriormente elimina las muertas-. Dentro del draw() se recorren todos los emisores, donde se agregan nuevas partículas, se actualizan y se dibujan las que ya fueron creadas. También como en el caso anterior hay un valor de "lifespan" que se reduce cada frame. Dentro del run del emisor, se hace el mismo recorrido inverso por las partículas para determinar su eliminación del Canvas.

>3. Para este tercer código, solo hay un emisor que se crea en la parte de arriba del Canvas. Ese emisor es el que tiene el arreglo interno de partículas -es decir, donde son generadas y guardadas-, pero este con un random decide si crea un partícula normal o una tipo "confetti", que viene desde la clase con su mismo nombre, pero está hereda -es decir, es una hija- de una clase particle.js. En esta clase confetti.js, se usa un show() que sirve para darle la forma que se desea y en este caso se quiso representar como un cuadrado que rota. En el draw() hace lo mismo que las demás, genera, guarda, actualiza y comprueba -si está muerta-, por medio de un "for inverso". Conserva también la misma lógica del "lifespan"

>4. En este cuarto código, también se tiene un solo emisor con un arreglo de generación y guardado de partículas. Dentro de las partículas, ya no solo hay un "lifespan", sino también una mass -masa- que permite recibir fuerzas externas. En cada frame se aplica una fuerza que afecta a cada partícula en base a su masa. Su generación, guardado, actualización, dibujo y posterior eliminación funciona de la misma manera que las anteriormente mencionadas.

>5. Este último código tiene también un solo emisor y se agrega un objeto nuevo llamado "Repeller", que funciona como una fuerza de repulsión -las aleja según la distancia, cuánto mas cerca, más fuerte la empuja; por medio de un logaritmo parecido a la gravedad pero a la inversa- que afecta cada partícula, además de ser afectadas desde un principio por la fuerza de gravedad del anterior código. El emisor en este caso también es el encargado de generar las partículas en cada frame, el draw() sigue funcionando igual que los demás casos y las partículas siguen conservando su "lifespan" para detereminar su estado de vida.

## Parte 2.
Ahora, vamos a probar con los experimentos:

* 1. __4.2: an Array of Particles.__
>Apliqué distribución gaussiana en la generación -en el eje X- de las partículas, con el proposito de que se sintiera como una cortina de lluvia. Solo tuve dos valores, uno que permite ubicarse en la mitad del ancho -centro del Canvas- y otro que contiene una desviación estándar para que así se permita recorrer espacios amplios en el eje X. Al ser Gaussiana solo se usa un RandomGaussian que el X es manipulado por estos dos valores anteriormente mencionados y el "y" solo se deja por "y", ya no que queremos afectar la altura. Ya es el mismo Gaussiano quien se encarga de recorrer el espacio de forma suave y con cierta variabilidad.

## Enlace a la obra en el editor de p5.js
[Aquí está mi experimento](https://editor.p5js.org/JuanJAreiza/sketches/SP_giaq_n)

## Código de la obra 

``` js
let particles = [];

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);
  particles.push(new Particle(width / 2, 20));

  // Looping through backwards to delete
  for (let i = particles.length - 1; i >= 0; i--) {
    let particle = particles[i];
    particle.run();
    if (particle.isDead()) {
      //remove the particle
      particles.splice(i, 1);
    }
  }
}

function keyPressed() {
 if (key === 'S' || key === 's') saveCanvas('experimento', 'jpg');
}

class Particle {
  constructor(x, y) {
    // Cambio la posición X de generación usando distribución gaussiana
    let center = width / 2; // buscando el centro de la pantalla
    let desvia = 60; // la desviación estándar
    this.position = createVector(randomGaussian(center, desvia), y);

    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  // Method to update position
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  // Method to display
  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  // Is the particle still useful?
  isDead() {
    return (this.lifespan < 0.0);
  }
}

```

## Captura de pantalla representativa
![experimento](https://github.com/user-attachments/assets/c7df9b9c-a617-4621-a33e-35f5491c60ef)

----------------------------------------------------------------------------

* 2. __4.4: a System of Systems.__
>En este caso apliqué Perlin para simular una fuerza de viento sobre las partículas, parecido a los dientes de león (creo que así se llaman). Lo hice creando un valor de ruido que varía en el tiempo y usándolo como componente horizontal de una fuerza que se aplica a cada partícula.

## Enlace a la obra en el editor de p5.js
[Aquí está mi experimento](https://editor.p5js.org/JuanJAreiza/sketches/kcjj2Eykl)

## Código de la obra 

``` js
let emitters = [];
let t = 0; // tiempo para Perlin

function setup() {
  createCanvas(640, 240);
  let text = createP("click to add particle systems");
}

function draw() {
  background(255);
  for (let emitter of emitters) {
    emitter.run();
    emitter.addParticle();
  }
  t += 0.5; // avanza el tiempo para el ruido
}

function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}

function keyPressed() {
 if (key === 'S' || key === 's') saveCanvas('experimento', 'jpg');
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    
    // Velocidad inicial estándar
    this.velocity = createVector(random(-1, 1), random(-1, 0));

    this.lifespan = 255.0;
    this.noiseOffset = random(1000); // offset único para cada partícula
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    
    // Dirección influenciada por Perlin noise (simula viento)
    let angle = noise(this.noiseOffset, t) * TWO_PI * 2;
    let wind = p5.Vector.fromAngle(angle).mult(0.1);
    this.applyForce(wind);
    
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  // Method to update position
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  // Method to display
  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  // Is the particle still useful?
  isDead() {
    return this.lifespan < 0.0;
  }
}
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  run() {
    // Looping through backwards to delete
    for (let i = this.particles.length - 1; i >= 0; i--) {
      this.particles[i].run();
      if (this.particles[i].isDead()) {
        // Remove the particle
        this.particles.splice(i, 1);
      }
    }
  }
}
```

## Captura de pantalla representativa
![experimento](https://github.com/user-attachments/assets/53e550c8-c467-4051-8f1a-e844b11dc885)

----------------------------------------------------------------------------

* 3. __4.5: a Particle System with Inheritance and Polymorphism.__
>En este tercer caso apliqué el concepto de LerpColor. Hice que cada partícula (tanto normal como confetti) interpole su color en basa al largo de su vida (con el lifespan). El confetti cuadrado maneja colores de naranja a amarillo, mientras que los circulares de azul a blanco.

## Enlace a la obra en el editor de p5.js
[Aquí está mi experimento](https://editor.p5js.org/JuanJAreiza/sketches/I72oJILVD)

## Código de la obra 

``` js
let emitter;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 20);
}

function draw() {
  background(255);
  emitter.addParticle();
  emitter.run();
}

function keyPressed() {
 if (key === 'S' || key === 's') saveCanvas('experimento', 'jpg');
}
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.lifespan = 255.0;

    // Colores inicial y final para LerpColor
    this.startColor = color(0, 150, 255);   // azul brillante
    this.endColor = color(255, 255, 255);   // blanco
  }

  run() {
    let gravity = createVector(0, 0.05);
    this.applyForce(gravity);
    this.update();
    this.show();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    // Usamos el lifespan como interpolador
    let amt = map(this.lifespan, 255, 0, 0, 1);
    let col = lerpColor(this.startColor, this.endColor, amt);

    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(col);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    let r = random(1);
    if (r < 0.5) {
      this.particles.push(new Particle(this.origin.x, this.origin.y));
    } else {
      this.particles.push(new Confetti(this.origin.x, this.origin.y));
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let p = this.particles[i];
      p.run();
      if (p.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
class Confetti extends Particle {
  constructor(x, y) {
    super(x, y);
    // Paleta distinta para confetti
    this.startColor = color(255, 100, 0);   // naranja
    this.endColor = color(255, 255, 0);     // amarillo
  }

  show() {
    let angle = map(this.position.x, 0, width, 0, TWO_PI * 2);
    let amt = map(this.lifespan, 255, 0, 0, 1);
    let col = lerpColor(this.startColor, this.endColor, amt);

    rectMode(CENTER);
    fill(col);
    stroke(0, this.lifespan);
    strokeWeight(2);
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);
    square(0, 0, 12);
    pop();
  }
}
```

## Captura de pantalla representativa
![experimento](https://github.com/user-attachments/assets/fce22736-0d14-42ac-8cc5-27bd9339d094)

----------------------------------------------------------------------------

* 4. __4.6: a Particle System with Forces.__
>Para este penúltimo experimento apliqué Lévy Flight. Además de la gravedad, cada partícula recibe una fuerza horizontal extra que se genera gracias a este. la mayor parte del tiempo se mueve suavemente a los lados, pero de repente puede hacer un movimiento brusco.

## Enlace a la obra en el editor de p5.js
[Aquí está mi experimento](https://editor.p5js.org/JuanJAreiza/sketches/4BhGVEXAA)

## Código de la obra 

``` js
let emitter;

function setup() {
  createCanvas(1280, 480);
  emitter = new Emitter(width / 2, 50);
}

function draw() {
  background(255, 30);

  // Fuerza de gravedad
  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  // Lévy Flight como fuerza horizontal
  let step = levyFlight();
  let levyForce = createVector(step * 0.05, 0); // fuerza horizontal
  emitter.applyForce(levyForce);

  emitter.addParticle();
  emitter.run();
}

function levyFlight() {
  let r = random(1);
  if (r < 0.9) {
    return random(-2, 2);  // pasos cortos la mayoría de veces
  } else {
    return random(-20, 20); // salto largo en raras ocasiones
  }
}

function keyPressed() {
 if (key === 'S' || key === 's') saveCanvas('experimento', 'jpg');
}
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.acceleration = createVector(0, 0.0);
    this.velocity = createVector(random(-1, 1), random(-2, 0));
    this.lifespan = 255.0;
    this.mass = 1;
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(force) {
    let f = force.copy();
    f.div(this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    this.lifespan -= 2.0;
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, this.mass * 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}
class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```

## Captura de pantalla representativa
![experimento](https://github.com/user-attachments/assets/7ec1be71-9be1-412c-a0bd-40bde5bb144b)

----------------------------------------------------------------------------

* 5. __4.7: a Particle System with a Repeller.__
>En este último caso apliqué Resistencia de agua. Lo añadí como una fuerza de fricción proporcional a la velocidad de cada partícula, pero en dirección contraria. Lo hice porque se me ocurrió interpretar las partículas como peces que esquivan un depredador, entonces con el fin de imitar el fondo marino, me pareció idóneo.

## Enlace a la obra en el editor de p5.js
[Aquí está mi experimento](https://editor.p5js.org/JuanJAreiza/sketches/DKuqlQETS)

## Código de la obra 

``` js
let emitter;
let repeller;

function setup() {
  createCanvas(640, 240);
  emitter = new Emitter(width / 2, 60);
  repeller = new Repeller(width / 2, 200);
}

function draw() {
  background(255);

  emitter.addParticle();

  // Gravedad universal
  let gravity = createVector(0, 0.1);
  emitter.applyForce(gravity);

  // Resistencia del aire/agua
  emitter.applyDrag(0.05); // coeficiente de fricción

  // Repulsor
  emitter.applyRepeller(repeller);

  emitter.run();
  repeller.show();
}

function keyPressed() {
 if (key === 'S' || key === 's') saveCanvas('experimento', 'jpg');
}
class Repeller {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.power = 150;
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 32);
  }

  repel(particle) {
    let force = p5.Vector.sub(this.position, particle.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 50);
    let strength = (-1 * this.power) / (distance * distance);
    force.setMag(strength);
    return force;
  }
}
class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector(random(-1, 1), random(-1, 0));
    this.acceleration = createVector(0, 0);
    this.lifespan = 255.0;
  }

  run() {
    this.update();
    this.show();
  }

  applyForce(f) {
    this.acceleration.add(f);
  }

  // Resistencia de aire/agua
  applyDrag(c) {
    let drag = this.velocity.copy();
    drag.mult(-1); // dirección contraria a la velocidad
    let speedSq = this.velocity.magSq();
    drag.setMag(c * speedSq); // magnitud proporcional al cuadrado de la velocidad
    this.applyForce(drag);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.lifespan -= 2;
    this.acceleration.mult(0);
  }

  show() {
    stroke(0, this.lifespan);
    strokeWeight(2);
    fill(127, this.lifespan);
    circle(this.position.x, this.position.y, 8);
  }

  isDead() {
    return this.lifespan < 0.0;
  }
}

class Emitter {
  constructor(x, y) {
    this.origin = createVector(x, y);
    this.particles = [];
  }

  addParticle() {
    this.particles.push(new Particle(this.origin.x, this.origin.y));
  }

  applyForce(force) {
    for (let particle of this.particles) {
      particle.applyForce(force);
    }
  }

  applyDrag(c) {
    for (let particle of this.particles) {
      particle.applyDrag(c);
    }
  }

  applyRepeller(repeller) {
    for (let particle of this.particles) {
      let force = repeller.repel(particle);
      particle.applyForce(force);
    }
  }

  run() {
    for (let i = this.particles.length - 1; i >= 0; i--) {
      const particle = this.particles[i];
      particle.run();
      if (particle.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}
```

## Captura de pantalla representativa
![experimento](https://github.com/user-attachments/assets/a30627dc-56c8-4763-8701-659f2959e98c)

//Todo sobre la creación y desaparición de las partículas lo expliqué en la primera parte.//

## Parte 3.
### Apply.

* __Descripción del Diseño de la obra__
La obra se llama __"Columpios del Azar"__. La idea es una hilera de péndulos/columpios colgando del techo que, al balancearse, generan partículas. Esas partículas no son solo “puntos que caen”: unas son pequeños circulos que siguen el vaivén del péndulo, otras son cometas que dejan rastro y otras burbujas que flotan suavemente. Quiero que la obra sea clara en su ritmo propio de un péndulo y las variaciones en cada partícula que lo hace sentir vivo. Es un contraste entre lo uniforme y lo "caótico".

Me imagino su interactividad como la herramienta y posibilidad al usuario de crear mas péndulos por el espacio y cambiar sus colores (por predefinidos) cuando desee.

__Sus controles son:__
>S para guardar.
>P para cambiar la paleta de color.
>C para limpiar el Canva y empezar desde cero.

__Conceptos que utilicé:__
>Péndulos.
>LerpColor.
>Gravedad.
>Motion 101.
>Random.

## Enlace a la obra en el editor de p5.js
[Aquí está mi obra](https://editor.p5js.org/JuanJAreiza/sketches/a0aXtJm14)

## Código de la obra 

``` js
// "Columpios del Azar"

let pendulums = [];   // array con emisores (pivotes)
let palettes = [];
let palIndex = 0;

function setup() {
  createCanvas(960, 540);
  colorMode(RGB);
  // definimos paletas
  palettes = [
    { a: color(255, 150, 90), b: color(255, 240, 210) },
    { a: color(90, 150, 255), b: color(200, 230, 255) },
    { a: color(160, 255, 200), b: color(220, 255, 240) }
  ];

  // crear algunos péndulos iniciales
  let spacing = width / 6;
  for (let i = 1; i <= 4; i++) {
    let x = i * spacing;
    pendulums.push(new PendulumEmitter(x, 80, random(90, 220)));
  }
}

function draw() {
  // fondo con leves trails, siempre corriendo (sin pause)
  background(18, 22, 30, 18);

  // instrucciones
  noStroke();
  fill(255, 180);
  textSize(12);
  text("Click = Agregar péndulo | Arrastra el mouse cerca de un péndulo para empujarlo | L = Limpiar Canva | P = Cambiar paleta de colores | S = Pantallazo de la obra", 10, height - 12);

  // actualizar y dibujar cada péndulo (siempre emiten)
  for (let p of pendulums) {
    p.run();
    p.emit();
  }
}

function mousePressed() {
  // nuevo péndulo en X del mouse
  pendulums.push(new PendulumEmitter(mouseX, 80, random(80, 260)));
}

function keyPressed() {
  if (key === 'L' || key === 'l') {
    pendulums = [];
  }
  if (key === 'P' || key === 'p') palIndex = (palIndex + 1) % palettes.length;
  
  if (key === 'S' || key === 's') saveCanvas('obraUnidad5', 'jpg');
}

// -------------------- PendulumEmitter --------------------
class PendulumEmitter {
  // x,y = pivot position; len = cord length
  constructor(x, y, len) {
    this.anchor = createVector(x, y);
    this.len = len;
    // parámetros del péndulo (ángulo inicial aleatorio)
    this.angle = random(-PI/6, PI/6);
    this.aVel = 0;
    this.aAcc = 0;
    this.damping = 0.995; // amortiguamiento angular
    this.rate = 2; // particles per frame
    this.particles = [];
    this.max = 25;
    // estética
    this.highlighted = false;
    // paleta local (se actualiza con la global al emitir)
    let pal = palettes[palIndex];
    this.colorFrom = pal.a;
    this.colorTo = pal.b;
  }

  emit() {
    if (this.particles.length > this.max) return;
    for (let i = 0; i < this.rate; i++) {
      // probabilidad para tipo
      let r = random();
      let p;
      if (r < 0.35) p = new PendulumBall(this.getBobPos().x, this.getBobPos().y, this);
      else if (r < 0.55) p = new Comet(this.getBobPos().x, this.getBobPos().y);
      else if (r < 0.7) p = new Bubble(this.getBobPos().x, this.getBobPos().y);
      else p = new ColorShifter(this.getBobPos().x, this.getBobPos().y);

      // asignar paleta actual
      let pal = palettes[palIndex];
      p.startCol = pal.a;
      p.endCol = pal.b;
      this.particles.push(p);
    }
  }

  applyPush(strength) {
    // Empuje al péndulo: modificar velocidad angular
    this.aVel += strength;
  }

  getBobPos() {
    // posición actual del extremo del péndulo según angle
    let x = this.anchor.x + this.len * sin(this.angle);
    let y = this.anchor.y + this.len * cos(this.angle);
    return createVector(x, y);
  }

  run() {
    // detectar mouse cerca para highlight y push
    let dToMouse = dist(mouseX, mouseY, this.anchor.x, this.anchor.y);
    this.highlighted = (dToMouse < 160);

    // física del péndulo: angularAcceleration = - (g / L) * sin(angle)
    let g = 0.8;
    this.aAcc = - (g / this.len) * sin(this.angle);
    // si mouse está cerca y presiono, aplica pequeño empuje
    if (this.highlighted && mouseIsPressed) {
      let dir = (mouseX > this.anchor.x) ? 0.06 : -0.06;
      this.aAcc += dir * map(dToMouse, 0, 160, 1, 0.1);
    }

    // integrar (Motion101) - siempre
    this.aVel += this.aAcc;
    this.aVel *= this.damping;
    this.angle += this.aVel;

    // dibujar cuerda + bob
    let bob = this.getBobPos();
    stroke(200, 150);
    strokeWeight(1.2);
    line(this.anchor.x, this.anchor.y, bob.x, bob.y);

    noStroke();
    let bobCol = this.highlighted ? color(255, 230, 160) : color(220, 220, 240);
    fill(bobCol);
    circle(bob.x, bob.y, 8);

    fill(180);
    circle(this.anchor.x, this.anchor.y, 6);

    // actualizar y dibujar partículas asociadas
    for (let i = this.particles.length - 1; i >= 0; i--) {
      let pt = this.particles[i];
      // influencia del péndulo al nacer
      pt.applyInfluence(this.aVel * 0.2);
      pt.run();

      // Si la partícula murió (por vida o por salirse del canvas), eliminarla
      if (pt.isDead()) {
        this.particles.splice(i, 1);
      }
    }
  }
}

// -------------------- Particle base --------------------
class Particle {
  constructor(x, y) {
    this.reset(x, y);
  }

  reset(x, y) {
    this.position = createVector(x + random(-3,3), y + random(-3,3));
    this.velocity = createVector(random(-0.6,0.6), random(-1.2, -0.2)); // Motion101 basic
    this.acceleration = createVector(0, 0);
    this.lifespan = 200 + random(-30, 30);
    this.mass = random(0.6, 1.6);
    this.startCol = color(200, 220, 255);
    this.endCol = color(255, 240, 210);
    this.size = random(3, 8);
    this.phase = random(TWO_PI);
  }

  applyForce(f) {
    // F = ma
    let force = f.copy().div(this.mass);
    this.acceleration.add(force);
  }

  applyInfluence(str) {
    // influence applied by pendulum at birth
    this.applyForce(createVector(str * random(0.5,1.2), 0));
  }

  update() {
    // Motion 101 Euler integration
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
    // life decay
    this.lifespan -= 1.6;
  }

  isDead() {
    // Muere si la vida se acabó o si sale completamente del canvas
    if (this.lifespan <= 0) return true;
    if (this.position.x < 0 || this.position.x > width || this.position.y < 0 || this.position.y > height) return true;
    return false;
  }

  run() {
    this.update();
    this.show();
  }

  show() {
    let t = map(this.lifespan, 0, 250, 0, 1);
    t = constrain(t, 0, 1);
    let col = lerpColor(this.endCol, this.startCol, t);
    fill(red(col), green(col), blue(col), map(this.lifespan, 0, 250, 0, 255));
    noStroke();
    circle(this.position.x, this.position.y, this.size);
  }
}

// -------------------- PendulumBall (hereda Particle) --------------------
class PendulumBall extends Particle {
  constructor(x, y, emitterRef) {
    super(x, y);
    this.emitter = emitterRef; // referencia al péndulo que la lanzó
    this.size = random(4, 9);
    this.mass = random(0.6, 1.4);
    this.phase = random(TWO_PI);
  }

  run() {
    this.applyForce(createVector(0, 0.05 * this.mass));
    this.velocity.mult(0.995);
    this.update();

    if (this.emitter) {
      let bob = this.emitter.getBobPos();
      let tether = p5.Vector.sub(bob, this.position).mult(0.002);
      this.applyForce(tether);
    }

    this.show();
  }

  show() {
    let lifePct = map(this.lifespan, 0, 250, 0, 1);
    let col = lerpColor(this.endCol, this.startCol, lifePct);
    fill(red(col), green(col), blue(col), map(this.lifespan, 0, 250, 0, 255));
    noStroke();
    circle(this.position.x, this.position.y, this.size);
  }
}

// -------------------- Comet (rápida con rastro) --------------------
class Comet extends Particle {
  constructor(x, y) {
    super(x, y);
    this.size = random(3, 6);
    this.mass = random(0.4, 0.9);
    this.trail = [];
    this.velocity = createVector(random(-2, 2), random(-3, -1));
    this.lifespan = random(50, 100);
  }

  run() {
    this.applyForce(createVector(0, 0.06 * this.mass));
    if (random() < 0.02) this.applyForce(createVector(random(-0.3,0.3), 0));
    this.update();

    this.trail.push(this.position.copy());
    if (this.trail.length > 12) this.trail.shift();

    this.show();
  }

  show() {
    noFill();
    strokeWeight(1.5);
    for (let i = 0; i < this.trail.length; i++) {
      let p = this.trail[i];
      let a = map(i, 0, this.trail.length - 1, 20, 160);
      stroke(200, 210, 255, a);
      circle(p.x, p.y, this.size + i * 0.4);
    }
    noStroke();
    let col = lerpColor(this.endCol, this.startCol, map(this.lifespan, 0, 250, 0, 1));
    fill(red(col), green(col), blue(col), 255);
    circle(this.position.x, this.position.y, this.size * 1.4);
  }
}

// -------------------- Bubble (flota, suave) --------------------
class Bubble extends Particle {
  constructor(x, y) {
    super(x, y);
    this.size = random(6, 14);
    this.mass = random(0.8, 1.6);
    this.lifespan = random(120, 220);
    this.velocity = createVector(random(-0.4, 0.4), random(-1.4, -0.2));
  }

  run() {
    this.applyForce(createVector(0, -0.02 * this.mass));
    this.applyForce(createVector(sin(frameCount * 0.02 + this.phase) * 0.003, 0));
    this.update();
    this.show();
  }

  show() {
    let col = lerpColor(this.endCol, this.startCol, map(this.lifespan, 0, 250, 0, 1));
    noStroke();
    fill(red(col), green(col), blue(col), map(this.lifespan, 0, 250, 0, 180));
    circle(this.position.x, this.position.y, this.size);
  }
}

// -------------------- ColorShifter (usa LerpColor de rosa a morado y viceversa) --------------------
// -------------------- ColorShifter (flota lento, cambia de color y deja estela) --------------------
class ColorShifter extends Particle {
  constructor(x, y) {
    super(x, y);
    this.size = random(6, 12);
    this.mass = random(0.6, 1.2);
    this.lifespan = random(140, 200);
    this.maxLifespan = this.lifespan; // para mapear t correctamente
    this.trail = [];

    // Colores bien definidos
    if (palIndex % 2 === 0) {
      this.startCol = color(255, 80, 180);   // rosa vibrante
      this.endCol = color(100, 70, 255);     // morado vibrante
    } else {
      this.startCol = color(100, 70, 255);
      this.endCol = color(255, 80, 180);
    }

    this.velocity = createVector(random(-0.2, 0.2), random(-0.5, -0.1));
  }

  run() {
    this.applyForce(createVector(0, -0.01 * this.mass));
    this.applyForce(createVector(sin(frameCount * 0.03 + this.phase) * 0.002, 0));
    this.update();

    this.trail.push(this.position.copy());
    if (this.trail.length > 15) this.trail.shift();

    this.show();
  }

  show() {
    let t = map(this.lifespan, 0, this.maxLifespan, 0, 1);
    t = constrain(t, 0, 1);
    let baseCol = lerpColor(this.endCol, this.startCol, t);

    // Estela
    noFill();
    for (let i = 0; i < this.trail.length; i++) {
      let p = this.trail[i];
      let alpha = map(i, 0, this.trail.length - 1, 30, 100);
      let sz = map(i, 0, this.trail.length - 1, this.size * 0.2, this.size);
      stroke(red(baseCol), green(baseCol), blue(baseCol), alpha);
      circle(p.x, p.y, sz);
    }

    // Partícula principal
    let alpha = map(this.lifespan, 0, this.maxLifespan, 0, 255);
    noStroke();
    fill(red(baseCol), green(baseCol), blue(baseCol), alpha);
    circle(this.position.x, this.position.y, this.size);
  }
}
```

* __Captura de pantalla representativa__
![obraUnidad5](https://github.com/user-attachments/assets/90c31973-bb19-4575-86b3-b0e459b73699)


