# Evidencias de la unidad 6

## Actividades

* __Actividad 1.__ De las obras de Tyler Hobbs, ¿cuáles te llamen la atención y por qué? ¿Qué te inspira de su trabajo?:
> <img width="900" height="598" alt="Captura de pantalla 2025-09-24 091052" src="https://github.com/user-attachments/assets/243ac39c-75a5-4382-85f1-ab3265d1a928" />
> <img width="747" height="559" alt="Captura de pantalla 2025-09-24 091410" src="https://github.com/user-attachments/assets/746a1436-daac-480b-a0df-9f63749ab5a2" />

> Estas dos obras fueron las más atractivas para mi, principalmente por el estilo tan remarcado que tiene cada una.
> Por un lado, tenemos unos trazos muy órganicos, como simulando el producto de un pincel con pintura. Por algún motivo me da vibras con sus patrones, colores y la textura, de una pintura asiatica de los 80's. Sus patrones son 

> Del mismo modo, la segunda obra me atrae principalmente por la técnica usando puntos. Los patrones que se crean me parecen muy interesantes con cada evolución de los colores y respetando el espacio de cada elemento, siendo consciente de corregir la posibilidad de que se sobreescriban.

*  __Actividad 2.__:
> Un __steering force__ es un vector que indica hacía donde debe dirigirse y de qué manera debe de hacer ese trayecto un agente que está siendo influenciado por un "deseo" u objetivo. Este resulta en una fórmula "steering = deseo - velocidad (la cual inicialmente está influenciado el agente)", que permite crear un movimiento órganico y suave del objeto en cuestión.

> Su diferencia principal es que es una fuerza que no simula partícularmente ningún fénomeno físico, sino que en cambio es artificial. Su "simulación" vendría siendo el comportamiento de decisión propio del agente, como si tuviese algún tipo de inteligencia natural con deseos e intenciones.

> Craig Reynolds es el pionero de la simulación del comportamiento autónomo y el que introdujo el concepto de "Boids" en 1986, que refiere al comportamiento colectivo y coordinado que se puede observar en bandadas de pájaros o peces. Él usó diversas fuerzas de dirección para lograr comportamientos complejos y emergentes como:

> Separación: evitar chocar con otros boids.

> Alineación: mover en la misma dirección que los boids cercanos.

> Cohesión: moverse hacia el centro de masa del grupo.

> Estas reglas se implementan como fuerzas de dirección que se suman y afectan la velocidad y trayectoria del agente.

* Actividad 3:
> 1. El campo se guarda como una matriz en dos dimensiones. Es como si fuera un tablero que cubre toda la pantalla y cada casilla del tablero guarda un vector que apunta en cierta dirección; eso quiere decir que el tablero funciona en base al tamaño del Canvas. Ahora, esos vectores no son totalmente aleatorios -si se quiere-, sino que se generan con Perlin noise -en el código original-, que da cambios suaves y continuos. Eso hace que el flujo parezca natural, como si fueran corrientes de agua o viento.

> 2. Cada agente revisa en qué casilla de la cuadrícula está parado según su posición en la pantalla. Luego toma el vector guardado en esa celda y lo convierte en su “velocidad deseada”. Después, compara esa velocidad deseada con la que ya tiene y la diferencia se convierte en la fuerza de dirección. Esa fuerza le dice cuánto debe girar o corregir su rumbo. Todo se limita con un maxforce para que los giros no sean imposibles y se mantenga un movimiento suave.

> 3. __Resolución:__ es el que define el tamaño de cada casilla del campo. __Maxspeed:__ la velocidad máxima que un agente puede alcanzar. __Maxforce:__ la fuerza máxima con la que un agente puede corregir su trayectoria.

> 4. La modificación que hice al código original fue muy básico. Tomé la idea de modificar la resolución del campo y lo que hice fue disminuirla significativamente a 5. Este cambio provocó que aumentara el número de celdas en el canvas y por ende, hubiese más vectores.
Esto logró que los agentes tuvieran un movimiento más "erratico". Se veían cambiar mas bruscamente de dirección e incluso parecian temblar mientras se desplazaban, pero aún así, el movimiento se ve mas variado y alocado.

> La sección modificada:

> Antes:
``` js
flowfield = new FlowField(80);
```

> Después:
``` js
flowfield = new FlowField(5);
```
> Captura de pantalla con los vectores activados para ver:
![experimento (2)](https://github.com/user-attachments/assets/c5a3b522-b10d-4bfc-98a0-fb7b92efdd9a)

* Actividad 4:
> 1.1. __Separación:__ El objetivo es __evitar el amontonamiento y las colisiones__. El boid mira a los vecinos que están demasiado cerca (d < desiredSeparation) y calcula un vector que apunta lejos de cada vecino, que cambia por lo cerca que están (cuanto más cerca, más fuerza). Suma esos vectores, saca un promedio y lo convierte en una fuerza de steering restando la velocidad actual y limitando por maxforce.
> 1.2. __Alineación:__ Busca que los boids __vayan en la misma dirección__ promedio. Para eso el boid toma las velocidades de los vecinos dentro de un radio (neighborDistance), las promedia, normaliza y las escala a la maxspeed. La fuerza de steering es la diferencia entre ese vector deseado y la velocidad actual, limitada por maxforce. Finalmente da la sensación de que el grupo __comparte una dirección general__.
> 1.3. __Cohesión:__ Su objetivo es __mantener al grupo junto__, acercando a cada boid al “centro” de sus vecinos. El boid calcula la posición promedio de los vecinos (dentro de neighborDistance) y luego usa seek hacia ese punto: eso crea un vector hacia el centro, lo normaliza a maxspeed, resta la velocidad actual y lo limita por maxforce. Así tienden a __reunirse en torno a un centro común__ entre todos.

> 2.1. __Radio de percepción:__ separación usa desiredSeparation = 25; alineación y cohesión usan neighborDistance = 50.

> 2.2. __Pesos / multiplicadores:__ en flock() se aplican con sep.mult(1.5), ali.mult(1.0), coh.mult(1.0). Cada elemento controla la influencia que tiene en todos los boids.

> 2.3. __Velocidad y fuerza máximas:__ this.maxspeed = 3 y this.maxforce = 0.05.

> También algo que se puede considerar como muy influyente es el número de boids iniciales.

> 3. En la función flock() __aumenté tanto la separación como la alineación__. Específicamente, pasé de sep.mult(1.5) a sep.mult(5.0) y de ali.mult(1.0) a ali.mult(2.0). Al darle tanto peso a la separación, los boids siguen evitando amontonarse, pero ahora la alineación fuerte hace que, aunque se alejen entre sí, todos tiendan a moverse en la misma dirección promedio. El resultado es que el enjambre se estira en formaciones más alargadas, casi como sub grupos que viajan juntos, pero con bastante espacio entre cada individuo.
> Visualmente ya no aparenta un grupo compacto, sino un grupo grande del que se desprenden nuevos sub grupos que siguen respetando la dirección, pero no la formación, hasta que luego mas adelante vuelven a unirse al enjambre.

> La sección modificada:

> Antes:
``` js
sep.mult(1.5);
ali.mult(1.0);
```

> Después:
``` js
sep.mult(5.0);
ali.mult(2.0);
```
> Captura de pantalla con los vectores activados para ver:
![experimento (5)](https://github.com/user-attachments/assets/d9792594-e826-46c8-9f50-a65039887fbc)


## Apply

> Mi obra se inspira en una mezcla de recuerdos y referencias acuáticas (la temática que elegí) que han marcado mi vida. Desde inspiración en videos virales de peces con colores hermosos, hasta los juguetes de mi infancia como los Aqua Rings, que con sus aros de colores y fondos llamativos me transmitían la sensación de un mundo psicodélico y divertido. También tomé elementos de películas como Buscando a Nemo o La Sirenita, que __evocaban la vida marina como un espacio mágico lleno de energía.__

> Quise traducir esas sensaciones a lo generativo, donde el movimiento nunca se detiene y el fondo tiene su propia independencia, como si todo siguiera su curso natural. Sin embargo, el usuario se convierte en un participante activo de esta experiencia, transformando la contemplación en interacción.

> La pieza está acompañada por la canción __“Should I Stay or Should I Go” de The Clash__, un tema que ha estado presente en mi vida desde la adolescencia y que decidí incorporar como un hilo narrativo. Cada cambio en la canción detona transformaciones visuales que, como una corriente submarina, van marcando la evolución de la obra y de la propia relación entre música, memoria y juego.

> https://github.com/user-attachments/assets/f80d63b2-a5ff-4c49-9e6e-7a61960fa1fa

> <img width="800" height="800" alt="image" src="https://github.com/user-attachments/assets/e1e3626d-184d-4d2b-985f-4d13ebc875d2" />


## Enlace a la obra en el editor de p5.js

[Aquí está mi obra](https://editor.p5js.org/JuanJAreiza/sketches/vecBSKWtv)

## Código de la obra 

``` js
// --- Parámetros de simulación ---
const WIDTH = 960;
const HEIGHT = 720;
const SIM_WIDTH = WIDTH;
const SIM_HEIGHT = HEIGHT;

const NUM_BOIDS = 100;
const MAX_SPEED = 4.0;
const MAX_FORCE = 0.18;
const PERCEPTION_RADIUS = 55;

const SEPARATION_WEIGHT = 1.9;
const ALIGNMENT_WEIGHT = 0.8;
const COHESION_WEIGHT = 0.7;

const INITIAL_CLUSTER_RADIUS = 50;
const TRAIL_LENGTH = 10;
const PREDATOR_SPAWN_OFFSET_AFTER_FLOCK = 8.0;
const ZOOM_DURATION = 12000; // ms
const INITIAL_ZOOM = 3.0;
const FINAL_ZOOM = 1.0;

const FPS = 30;

// FlowField params
const FLOW_COLS = 20;
const FLOW_ROWS = 20;
const FLOW_FORCE = 0.9; // magnitude multiplier for flow force
const FLOW_INFLUENCE_AT_START = 1.0;
const TRANSITION_SECONDS = 3.0; // fade duration (68 -> 71)
const FLOW_PHASE_END = 67.0; // seconds
const FLOCK_START = 68.0; // seconds

// velocidad * volumen (empieza en 145s)
const VELOCITY_VOLUME_START = 145.0; // seconds
const VELOCITY_VOLUME_MULT = 1.8; // factor scale applied to level (adjust)
const MAX_VOLUME_SPEED_MULT = 3.0; // cap speed to maxSpeed * this

// mouse depredador
const MOUSE_PREDATOR_START = 142.0; // 2:22 -> 142s
const MOUSE_EAT_RADIUS = 12; // world coords
const MOUSE_EVADE_WEIGHT = 3.0;

// Predator weighting constants
const PREDATOR_CHASE_WEIGHT = 1.5;
const PREDATOR_EVADE_WEIGHT = 2.5;

// multi-predator params
const PREDATOR_MAX = 5;
const PREDATOR_SPAWN_INTERVAL = 6.0; // seconds between spawns after first
const PREDATOR_BASE_SPEED = 4.5;
const PREDATOR_BASE_PERCEPTION = 180;
const PREDATOR_EAT_RADIUS = 14; // mundo coords: radio de "comer" para depredadores

// cooldown para comer (segundos)
const PREDATOR_EAT_COOLDOWN = 3.0;

// color drops (falling ring particles)
const COLOR_DROP_MIN_RADIUS = 4;
const COLOR_DROP_MAX_RADIUS = 18;

// START TIME for colorDrops = midpoint between FLOCK_START and MOUSE_PREDATOR_START
const COLOR_DROPS_START = (FLOCK_START + MOUSE_PREDATOR_START) / 2.0; // computed midpoint

// --- Glow de portal sobre trail ---
const TRAIL_GLOW_DURATION = 800;

// --- Estado global ---
let flock = [];
let predators = []; // múltiples depredadores
let predatorSpawnStarted = false;
let lastPredatorSpawnTime = 0;
let startTime = 0;
let paused = false;
let ended = false; // song ended flag

let currentZoom = INITIAL_ZOOM;
let cameraCenterWorld; // p5.Vector

let trailColors = [];
let mode = 0;

// --- Audio ---
let song, fft, amp;
let bass = 0, treble = 0, level = 0;

// --- Visual extras ---
let bgFish = [];
let bubbles = [];
let waves = [];
let portals = [];
let colorDrops = []; // falling colorful ring particles
let predatorRings = []; // rings emitted by predators when they eat

// glow interaction
let glow = false;
let glowStart = 0;
let glowDuration = 600;

// Flow field
let flowField;
let showFlowVectors = true;

// mouse depredador estado
let mousePredatorActive = false;

function preload() {
  song = loadSound("clash.mp3");
}

function setup() {
  createCanvas(WIDTH, HEIGHT);
  frameRate(FPS);
  colorMode(HSB, 360, 100, 100, 255);
  noStroke();

  cameraCenterWorld = createVector(SIM_WIDTH / 2, SIM_HEIGHT / 2);
  _generateTrailColors();

  fft = new p5.FFT(0.9, 512);
  amp = new p5.Amplitude();

  for (let i = 0; i < NUM_BOIDS; i++) {
    let angle = random(TWO_PI);
    let r = random(INITIAL_CLUSTER_RADIUS);
    let x = cameraCenterWorld.x + cos(angle) * r;
    let y = cameraCenterWorld.y + sin(angle) * r;
    flock.push(new Boid(x, y));
  }
  startTime = millis();

  flowField = new FlowField(FLOW_COLS, FLOW_ROWS, SIM_WIDTH / FLOW_COLS);

  for (let i = 0; i < 12; i++) bgFish.push(new BackgroundFish());

  document.oncontextmenu = () => false;
}

function _generateTrailColors() {
  trailColors = [];
  for (let i = 0; i < TRAIL_LENGTH; i++) {
    let t = i / max(1, TRAIL_LENGTH - 1);
    let h = lerp(200, 220, t);
    let s = lerp(90, 40, t);
    let b = lerp(100, 30, t);
    let a = lerp(220, 90, t);
    trailColors.push(color(h, s, b, a));
  }
}

function keyPressed() {
  if (key === ' ') {
    if (!song.isPlaying()) {
      // Reproducimos una sola vez para detectar el final correctamente
      song.play();
      // Cuando termine la canción, marcamos ended = true
      if (typeof song.onended === 'function') {
        song.onended(() => { ended = true; });
      }
      // reiniciamos timebase visual
      startTime = millis();
      ended = false;
    }
  } else if (keyCode === ESCAPE) {
    location.reload();
  } else if (key === 'p' || key === 'P') {
    paused = !paused;
    if (paused) {
      if (song.isPlaying()) song.pause();
    }
  } else if (key === 'm' || key === 'M') {
    mode = (mode + 1) % 3;
  } else if (key === 's' || key === 'S') {
    saveCanvas('Obra6', 'png');
  } else if (key === 'I' || key === 'i') {
    flowField.invert();
  } else if (key === 'V' || key === 'v') {
    showFlowVectors = !showFlowVectors;
  }
}


// ---------------- FlowField ----------------
class FlowField {
  constructor(cols, rows, cellSize) {
    this.cols = cols; this.rows = rows; this.cellSize = cellSize;
    this.field = new Array(cols * rows);
    this.zoff = random(10);
    this.dirMult = 1;
    this.noiseOffset = random(1000);
    this.update(0);
  }
  index(col, row) { return constrain(col, 0, this.cols-1) + constrain(row,0,this.rows-1) * this.cols; }
  update(treble) {
    this.zoff += 0.003;
    for (let y = 0; y < this.rows; y++) {
      for (let x = 0; x < this.cols; x++) {
        let nx = x / this.cols, ny = y / this.rows;
        let n = noise(nx * 1.6, ny * 1.6, this.zoff + this.noiseOffset);
        let baseAngle = n * TWO_PI * 2.0;
        let trebleOffset = map(treble, 0, 255, -PI/3, PI/3);
        let angle = (baseAngle + trebleOffset) * this.dirMult;
        let v = p5.Vector.fromAngle(angle); v.setMag(1);
        this.field[this.index(x,y)] = v;
      }
    }
  }
  lookup(worldPos) {
    let col = Math.floor(constrain(worldPos.x / this.cellSize, 0, this.cols - 1));
    let row = Math.floor(constrain(worldPos.y / this.cellSize, 0, this.rows - 1));
    let idx = this.index(col, row);
    return this.field[idx] ? this.field[idx].copy() : createVector(1,0);
  }
  invert() { this.dirMult *= -1; }
  drawVectors() {
    push();
    stroke(0, 0, 100);
    strokeWeight(1);
    for (let y = 0; y < this.rows; y++) {
      for (let x = 0; x < this.cols; x++) {
        let v = this.field[this.index(x,y)];
        if (!v) continue;
        let wx = (x + 0.5) * this.cellSize;
        let wy = (y + 0.5) * this.cellSize;
        let screenP = worldToScreen(createVector(wx, wy));
        let len = (this.cellSize * 0.35) * currentZoom;
        let ex = screenP.x + v.x * len;
        let ey = screenP.y + v.y * len;
        line(screenP.x, screenP.y, ex, ey);
        push();
        translate(ex, ey);
        rotate(atan2(v.y, v.x));
        noStroke();
        triangle(-4, 2, -4, -2, 0, 0);
        pop();
      }
    }
    pop();
  }
}

// ---------------- Boid ----------------
class Boid {
  constructor(x, y) {
    this.position = createVector(x, y);
    let angle = random(TWO_PI);
    this.velocity = p5.Vector.fromAngle(angle).mult(random(0.5, MAX_SPEED * 0.8));
    this.acceleration = createVector(0,0);
    this.maxSpeed = MAX_SPEED;
    this.maxForce = MAX_FORCE;
    this.perception = PERCEPTION_RADIUS;
    this.trail = [];
    this.baseHue = random(180,260);
    this.trailGlowUntil = 0;
    this.trailGlowDuration = TRAIL_GLOW_DURATION;
    this.trailGlowStrength = 1.0;
  }
  applyForce(f){ this.acceleration.add(f); }
  handleEdges(isWrapping) {
    const minX = 0, maxX = SIM_WIDTH, minY = 0, maxY = SIM_HEIGHT;
    if (isWrapping) {
      if (this.position.x < minX) this.position.x = maxX;
      else if (this.position.x > maxX) this.position.x = minX;
      if (this.position.y < minY) this.position.y = maxY;
      else if (this.position.y > maxY) this.position.y = minY;
    } else {
      let bounced = false;
      if (this.position.x < minX) { this.position.x = minX; this.velocity.x *= -0.6; bounced = true; }
      else if (this.position.x > maxX) { this.position.x = maxX; this.velocity.x *= -0.6; bounced = true; }
      if (this.position.y < minY) { this.position.y = minY; this.velocity.y *= -0.6; bounced = true; }
      else if (this.position.y > maxY) { this.position.y = maxY; this.velocity.y *= -0.6; bounced = true; }
      if (bounced) { this.velocity.mult(0.98); this.acceleration.mult(0); }
    }
  }
  update() {
    this.trail.push(this.position.copy());
    if (this.trail.length > TRAIL_LENGTH) this.trail.shift();
    this.velocity.add(this.acceleration);
    if (this.velocity.mag() > this.maxSpeed) this.velocity.setMag(this.maxSpeed);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }
  steer(desired){ let s = p5.Vector.sub(desired, this.velocity); if (s.mag()>this.maxForce) s.setMag(this.maxForce); return s; }
  separation(boids){ let steering=createVector(0,0), total=0; for (let other of boids){ let d=p5.Vector.dist(this.position, other.position); if (d>0 && d < this.perception/1.5){ let diff=p5.Vector.sub(this.position, other.position); if (diff.magSq()>0) diff.div(d*d); steering.add(diff); total++; } } if(total>0){ steering.div(total); if(steering.mag()>0) steering.setMag(this.maxSpeed); steering=this.steer(steering);} return steering; }
  alignment(boids){ let steering=createVector(0,0), total=0; for (let other of boids){ let d=p5.Vector.dist(this.position, other.position); if (d>0 && d < this.perception) { steering.add(other.velocity); total++; } } if(total>0){ steering.div(total); if(steering.mag()>0) steering.setMag(this.maxSpeed); steering=this.steer(steering);} return steering; }
  cohesion(boids){ let steering=createVector(0,0), total=0, center=createVector(0,0); for (let other of boids){ let d=p5.Vector.dist(this.position, other.position); if (d>0 && d < this.perception) { center.add(other.position); total++; } } if(total>0){ center.div(total); let desired=p5.Vector.sub(center, this.position); if(desired.mag()>0) desired.setMag(this.maxSpeed); steering=this.steer(desired);} return steering; }
  evade(predatorPos){ let steering=createVector(0,0); if(predatorPos){ let d=p5.Vector.dist(this.position, predatorPos); let evadeRadius=this.perception*1.8; if(d>0 && d<evadeRadius){ let desired=p5.Vector.sub(this.position, predatorPos).normalize(); desired.mult(this.maxSpeed * (evadeRadius / max(d,1))); steering=this.steer(desired); if(steering.mag()>this.maxForce*1.8) steering.setMag(this.maxForce*1.8); } } return steering; }
  flock(boids, predatorPos=null, audio={bass:0,treble:0,level:0}) {
    let neighbors=[], percSq=this.perception*this.perception;
    for (let other of boids) if (other!==this) if (p5.Vector.sub(this.position, other.position).magSq() < percSq) neighbors.push(other);
    let bassFactor = map(audio.bass,0,255,0.6,2.2);
    let sepW = SEPARATION_WEIGHT * bassFactor;
    let aliW = ALIGNMENT_WEIGHT * lerp(0.8,1.2, audio.level*5);
    let cohW = COHESION_WEIGHT;
    let sep=this.separation(neighbors), ali=this.alignment(neighbors), coh=this.cohesion(neighbors), evd=this.evade(predatorPos);
    this.applyForce(p5.Vector.mult(sep, sepW));
    this.applyForce(p5.Vector.mult(ali, aliW));
    this.applyForce(p5.Vector.mult(coh, cohW));
    this.applyForce(p5.Vector.mult(evd, PREDATOR_EVADE_WEIGHT));
  }
  draw(isFlowDominant){
    for (let i=0;i<this.trail.length;i++){
      let idx=this.trail.length-1-i;
      let pos=this.trail[idx];
      let colIndex=i; if(colIndex>=trailColors.length) colIndex=trailColors.length-1;
      let screenPos=worldToScreen(pos);
      let size=max(1,((TRAIL_LENGTH-i)/(TRAIL_LENGTH*1.5))*(6/currentZoom));
      let isGlowing = millis() < this.trailGlowUntil;
      if(isGlowing){
        let remaining = this.trailGlowUntil - millis();
        let t = constrain(remaining / this.trailGlowDuration, 0, 1);
        let glowFactor = 1 + (this.trailGlowStrength - 1) * t;
        size *= glowFactor;
        let baseCol = trailColors[colIndex];
        let h=hue(baseCol), s=saturation(baseCol), b=brightness(baseCol), a=alpha(baseCol);
        let newA = constrain(a * glowFactor,0,255);
        fill(h,s,b,newA);
      } else fill(trailColors[colIndex]);
      ellipse(screenPos.x, screenPos.y, size, size);
    }
    let screenPos = worldToScreen(this.position);
    let angle = atan2(this.velocity.y, this.velocity.x);
    let baseSize = 7;
    let size = max(2, baseSize / currentZoom);
    push();
    translate(screenPos.x, screenPos.y);
    rotate(angle);
    noStroke();
    if (isFlowDominant) fill(0,0,100,230);
    else {
      let trebleShift = map(treble,0,255,-20,40);
      let base = (this.baseHue + trebleShift + 360) % 360;
      if (glow && millis() - glowStart < glowDuration) {
        let t = (millis() - glowStart) / glowDuration; let pulse = sin(t * PI) * 25;
        fill((base + pulse + 360) % 360, 90, constrain(100, 30, 100), 220);
      } else fill(base,85,80,200);
    }
    for (let a=0;a<TWO_PI;a+=0.35){ let px=cos(a)*size; let py=sin(a)*size*0.6; ellipse(px,py,max(1,size*0.18),max(1,size*0.18)); }
    pop();
  }
}

// ---------------- Predator (multiforma, color reactivo por bass) ----------------
class Predator extends Boid {
  constructor(x, y, shapeType="triangle") {
    super(x,y);
    this.shapeType = shapeType; // 'triangle','square','pentagon','star','hexagon'
    this.baseHue = random(0,360);
    this.maxSpeed = PREDATOR_BASE_SPEED;
    this.perception = PREDATOR_BASE_PERCEPTION;
    this.maxForce = MAX_FORCE * 1.2;
    this.trail = [];
    // cooldown tracking (tiempo en segundos)
    this.lastEat = -Infinity;
    this.hue = this.baseHue;
  }
  chase(boids) {
    let steering=createVector(0,0), sum=createVector(0,0), total=0, percSq=this.perception*this.perception;
    for (let b of boids) {
      let d2 = p5.Vector.sub(this.position, b.position).magSq();
      if (d2 < percSq) { sum.add(b.position); total++; }
    }
    if (total>0) {
      let target = p5.Vector.div(sum, total);
      let desired = p5.Vector.sub(target, this.position);
      if (desired.mag()>0) desired.setMag(this.maxSpeed);
      steering = this.steer(desired);
    }
    return steering;
  }
  flock(boids) {
    let chaseForce = this.chase(boids);
    this.applyForce(p5.Vector.mult(chaseForce, PREDATOR_CHASE_WEIGHT));
  }
  updateHue(bassVal) {
    this.hue = (this.baseHue + map(bassVal, 0, 255, -60, 60) + 360) % 360;
  }
  drawShapeAt(screenX, screenY, size) {
    noStroke();
    fill(this.hue, 90, 80);
    push();
    translate(screenX, screenY);
    if (this.shapeType === "triangle") {
      beginShape(); vertex(size,0); vertex(-size/1.5,size/1.5); vertex(-size/1.5,-size/1.5); endShape(CLOSE);
    } else if (this.shapeType === "square") {
      rectMode(CENTER); rect(0,0,size*1.4,size*1.4);
    } else if (this.shapeType === "pentagon") {
      beginShape();
      for (let i=0;i<5;i++){ let a = TWO_PI * i/5 - PI/2; vertex(cos(a)*size, sin(a)*size); }
      endShape(CLOSE);
    } else if (this.shapeType === "hexagon") {
      beginShape();
      for (let i=0;i<6;i++){ let a = TWO_PI * i/6 - PI/2; vertex(cos(a)*size, sin(a)*size); }
      endShape(CLOSE);
    } else if (this.shapeType === "star") {
      beginShape();
      for (let i=0;i<10;i++){
        let r = (i%2===0) ? size : size*0.5;
        let a = TWO_PI * i/10 - PI/2; vertex(cos(a)*r, sin(a)*r);
      }
      endShape(CLOSE);
    }
    pop();
  }
  draw() {
    for (let i=0;i<this.trail.length;i++){
      let pos=this.trail[i];
      let screenPos=worldToScreen(pos);
      let s = max(2, (this.trail.length - i) / (this.trail.length * 1.2) * (8 / currentZoom));
      fill(this.hue, 90, 60, 160 * (1 - i/ max(1,this.trail.length)));
      ellipse(screenPos.x, screenPos.y, s, s);
    }
    let screenPos = worldToScreen(this.position);
    this.updateHue(bass);
    let size = max(6, 16 / currentZoom);
    this.drawShapeAt(screenPos.x, screenPos.y, size);
  }
  update() {
    this.trail.push(this.position.copy());
    if (this.trail.length > Math.max(2, Math.floor(TRAIL_LENGTH / 2))) this.trail.shift();
    super.update();
  }
}

// ---------------- PredatorRing (aro emitido por depredador al comer) ----------------
class PredatorRing {
  constructor(worldPos, startR, col) {
    this.pos = worldPos.copy();
    this.r = startR;
    this.growth = 6 + random(-1,1);
    this.alpha = 200;
    this.col = col; // p5 color
    this.lineWidth = 2.0;
  }
  update() {
    this.r += this.growth;
    this.alpha -= 5;
  }
  display() {
    let screenP = worldToScreen(this.pos);
    push();
    noFill();
    stroke(hue(this.col), saturation(this.col), brightness(this.col), this.alpha);
    strokeWeight(this.lineWidth / max(0.5, currentZoom));
    ellipse(screenP.x, screenP.y, this.r * 2 * currentZoom);
    pop();
  }
  isDead() { return this.alpha <= 0; }
}

// ---------------- ColorDrop (falling colorful rings influenced by bass) ----------------
class ColorDrop {
  constructor(x, radius) {
    this.pos = createVector(x, -10);
    this.r = radius;
    this.speed = random(0.6, 2.2);
    this.alpha = 200;
    this.hue = random(10, 320); // vivid range
    this.sat = random(80, 100);
    this.brt = random(80, 100);
  }
  update(bassVal) {
    let bassFactor = map(bassVal, 0, 255, 0.6, 2.5);
    this.pos.y += this.speed * bassFactor;
    this.alpha -= 1.6 + map(bassVal,0,255,0,1.4);
  }
  display() {
    noFill();
    let sw = constrain(1 + this.r * 0.08 / max(0.5, currentZoom), 1, 6);
    strokeWeight(sw);
    stroke(this.hue, this.sat, this.brt, this.alpha);
    ellipse(this.pos.x, this.pos.y, this.r*2);
    stroke(this.hue, this.sat, min(100, this.brt + 8), this.alpha * 0.5);
    strokeWeight(max(0.5, sw * 0.5));
    ellipse(this.pos.x, this.pos.y, this.r*1.4);
    noStroke();
  }
  isDead() { return this.alpha <= 0 || this.pos.y > height + this.r*2; }
}

// ---------------- Utilities ----------------
function worldToScreen(worldPos) {
  let relative = p5.Vector.sub(worldPos, cameraCenterWorld);
  let screenPos = relative.copy().mult(currentZoom).add(createVector(width/2, height/2));
  return screenPos;
}
function screenToWorld(sx, sy) {
  return createVector(cameraCenterWorld.x + (sx - width/2)/currentZoom, cameraCenterWorld.y + (sy - height/2)/currentZoom);
}

// BackgroundFish, Bubble, Wave, PortalPulse (mantengo)
class BackgroundFish { constructor(){ this.yBase = random(height*0.25, height*0.85); this.x = random(-100, width+100); this.speed = random(0.2,0.9); this.amp=random(6,30); this.freq=random(0.004,0.018); this.offset=random(TWO_PI); this.size=random(18,48); this.dir = random()<0.5?1:-1; if (this.dir===1) this.x=random(-width*0.4,-this.size); else this.x=random(width+this.size,width+width*0.4);} update(){ this.x += this.speed*this.dir; this.y = this.yBase + sin(frameCount*this.freq + this.offset)*this.amp; } display(){ push(); translate(this.x,this.y); scale(this.dir,1); noStroke(); fill(200,60,100,8); ellipse(0,0,this.size*2,this.size); triangle(-this.size,0,-this.size*1.5,-this.size*0.4,-this.size*1.5,this.size*0.4); pop(); } isOut(){ return (this.dir===1 && this.x > width + this.size*2) || (this.dir===-1 && this.x < -this.size*2); } }
class Bubble { constructor(x,y,r){ this.pos=createVector(x,y); this.r=r; this.speed=random(0.8,2); this.alpha=160;} update(){ this.pos.y -= this.speed; this.alpha -= 1.2;} display(){ noFill(); stroke(200,30,100,this.alpha); strokeWeight(1.5); ellipse(this.pos.x,this.pos.y,this.r*2);} isDead(){ return this.alpha<=0 || this.pos.y < -50; } }
class Wave { constructor(x,y,col){ this.pos=createVector(x,y); this.r=8; this.growth=3; this.alpha=180; this.col=col;} update(){ this.r+=this.growth; this.alpha-=2.0; } display(){ noFill(); stroke(hue(this.col), saturation(this.col), brightness(this.col), this.alpha); strokeWeight(2); ellipse(this.pos.x, this.pos.y, this.r*2);} isDead(){ return this.alpha<=0; } }
class PortalPulse { constructor(x,y){ this.x=x; this.y=y; this.r=6; this.alpha=200; this.growth=8;} update(){ this.r+=this.growth; this.alpha-=6; let worldCenter = createVector((cameraCenterWorld.x + (this.x - width/2)/currentZoom),(cameraCenterWorld.y + (this.y - height/2)/currentZoom)); let influenceR = this.r / currentZoom * 1.2; for (let b of flock){ let d = p5.Vector.dist(b.position, worldCenter); if (d < influenceR){ let dir = p5.Vector.sub(b.position, worldCenter).normalize(); let strength = map(d,0,influenceR,5,0.4); b.applyForce(dir.mult(strength*0.02)); let intensity = map(d,0,influenceR,1.9,1.15); b.trailGlowUntil = millis() + b.trailGlowDuration; b.trailGlowStrength = intensity; } } } display(){ noFill(); stroke(260,80,90,this.alpha); strokeWeight(2); ellipse(this.x,this.y,this.r);} isDead(){ return this.alpha<=0; } }

// ---------------- Main draw loop ----------------
function draw() {
  if (paused) {
    fill(0,140); rect(0,0,width,height); fill(255); textSize(18); textAlign(CENTER,CENTER); text("PAUSED — presiona 'P' para continuar", width/2, height/2); return;
  }

  // audio
  fft.analyze();
  bass = fft.getEnergy("bass");
  treble = fft.getEnergy("treble");
  level = amp.getLevel();

  // song time
  let songSec = 0;
  if (song && song.isLoaded && song.isPlaying && song.isPlaying()) songSec = song.currentTime();
  else songSec = (millis() - startTime) / 1000.0;

  // detect song end
  let songDuration = (song && song.duration && typeof song.duration === 'function') ? song.duration() : Infinity;
  if (songDuration !== Infinity && songSec >= songDuration && !ended) {
    ended = true;
    try { if (song.isPlaying()) song.stop(); } catch(e){}
  }
  if (ended) {
    background(0);
    push();
    fill(0,0,100);
    textAlign(CENTER, CENTER);
    textSize(36);
    textStyle(BOLD);
    text("Should I Stay or Should I go", width/2, height/2);
    pop();
    return;
  }

  // update flowField
  flowField.update(treble);

  // zoom
  let elapsedMs = millis() - startTime;
  if (elapsedMs < ZOOM_DURATION) {
    let progress = elapsedMs / ZOOM_DURATION;
    currentZoom = INITIAL_ZOOM + (FINAL_ZOOM - INITIAL_ZOOM) * progress;
  } else currentZoom = FINAL_ZOOM;

  let elapsed = songSec;

  // mouse predator active?
  mousePredatorActive = elapsed >= MOUSE_PREDATOR_START;
  let mouseWorld = null;
  if (mousePredatorActive) mouseWorld = screenToWorld(mouseX, mouseY);

  // background
  let bgHue = mode === 0 ? 210 : mode === 1 ? 280 : 140;
  background(bgHue, 30, 8);

  // predator spawn control
  let flockStartSec = FLOCK_START;
  let firstPredatorSpawnSec = flockStartSec + PREDATOR_SPAWN_OFFSET_AFTER_FLOCK;
  if (!predatorSpawnStarted && elapsed >= firstPredatorSpawnSec) {
    predatorSpawnStarted = true;
    lastPredatorSpawnTime = elapsed;
    spawnPredator(); // spawn first
  }
  if (predatorSpawnStarted && predators.length < PREDATOR_MAX && (elapsed - lastPredatorSpawnTime) >= PREDATOR_SPAWN_INTERVAL) {
    spawnPredator();
    lastPredatorSpawnTime = elapsed;
  }

  // update background fish
  for (let i = bgFish.length - 1; i >= 0; i--) {
    bgFish[i].update();
    bgFish[i].display();
    if (bgFish[i].isOut()) { bgFish.splice(i,1); bgFish.push(new BackgroundFish()); }
  }

  // existing bubble logic (bass-driven)
  if (bass > 170 && frameCount % 6 === 0) bubbles.push(new Bubble(random(width), height + 20, random(6,18)));
  for (let i = bubbles.length - 1; i >= 0; i--) { bubbles[i].update(); bubbles[i].display(); if (bubbles[i].isDead()) bubbles.splice(i,1); }

  // waves on treble peaks
  if (treble > 160 && frameCount % 12 === 0) waves.push(new Wave(random(width), random(height*0.55), color(map(treble,0,255,180,300), 70, 90)));
  for (let i = waves.length - 1; i >= 0; i--) { waves[i].update(); waves[i].display(); if (waves[i].isDead()) waves.splice(i,1); }

  // spawn colorDrops only AFTER COLOR_DROPS_START (midpoint)
  if (elapsed >= COLOR_DROPS_START) {
    let dropChance = map(bass, 0, 255, 0.01, 0.45);
    if (random() < dropChance && frameCount % 2 === 0) {
      let rx = random(width);
      let rr = random(COLOR_DROP_MIN_RADIUS, COLOR_DROP_MAX_RADIUS);
      colorDrops.push(new ColorDrop(rx, rr));
    }
  }
  for (let i = colorDrops.length - 1; i >= 0; i--) {
    colorDrops[i].update(bass);
    colorDrops[i].display();
    if (colorDrops[i].isDead()) colorDrops.splice(i,1);
  }

  // Determine flow/flock influence
  let flowInfluence = 0, flockInfluence = 0;
  if (elapsed <= FLOW_PHASE_END) { flowInfluence = FLOW_INFLUENCE_AT_START; flockInfluence = 0; }
  else if (elapsed >= FLOCK_START + TRANSITION_SECONDS) { flowInfluence = 0; flockInfluence = 1; }
  else if (elapsed >= FLOCK_START && elapsed < FLOCK_START + TRANSITION_SECONDS) {
    let t = map(elapsed, FLOCK_START, FLOCK_START + TRANSITION_SECONDS, 0, 1);
    flowInfluence = lerp(1,0,t); flockInfluence = lerp(0,1,t);
  } else if (elapsed > FLOW_PHASE_END && elapsed < FLOCK_START) {
    let t = map(elapsed, FLOW_PHASE_END, FLOCK_START, 0, 1);
    flowInfluence = lerp(1,1,t); flockInfluence = lerp(0,0,t);
  }

  let wrappingActive = elapsed < (FLOCK_START + TRANSITION_SECONDS);
  let audioState = {bass: bass, treble: treble, level: level};
  let predatorPos = predators.length > 0 ? predators[0].position : null;

  // boids loop (reverse for possible removal by mouse predator)
  for (let i = flock.length - 1; i >= 0; i--) {
    let b = flock[i];

    if (flowInfluence > 0.001) {
      let f = flowField.lookup(b.position);
      let fMag = FLOW_FORCE * lerp(0.8, 1.4, map(level, 0, 0.2, 0, 1));
      f.mult(fMag * flowInfluence);
      if (f.mag() > b.maxForce) f.setMag(b.maxForce * 1.2);
      b.applyForce(f);
    }

    if (flockInfluence > 0.001) {
      let prevAcc = b.acceleration.copy();
      b.flock(flock, predatorPos, audioState);
      let addedAcc = p5.Vector.sub(b.acceleration, prevAcc);
      addedAcc.mult(flockInfluence);
      b.acceleration = prevAcc.copy().add(addedAcc);
    }

    // mouse-evade
    if (mousePredatorActive && mouseWorld) {
      let ev = b.evade(mouseWorld);
      if (ev.mag() > 0) { ev.mult(MOUSE_EVADE_WEIGHT); b.applyForce(ev); }
    }

    b.update();

    // velocity-volume multiplier after VELOCITY_VOLUME_START
    if (elapsed >= VELOCITY_VOLUME_START) {
      let volMult = 1 + level * VELOCITY_VOLUME_MULT;
      b.velocity.mult(volMult);
      let cap = b.maxSpeed * MAX_VOLUME_SPEED_MULT;
      if (b.velocity.mag() > cap) b.velocity.setMag(cap);
    }

    // mouse eat
    if (mousePredatorActive && mouseWorld) {
      let d = p5.Vector.dist(b.position, mouseWorld);
      if (d <= MOUSE_EAT_RADIUS) {
        waves.push(new Wave(mouseX, mouseY, color(0,0,100)));
        flock.splice(i,1);
        continue;
      }
    }

    b.handleEdges(wrappingActive);
  }

  // predators update & eat (con cooldown)
  for (let pIndex = predators.length - 1; pIndex >= 0; pIndex--) {
    let p = predators[pIndex];
    p.flock(flock);
    p.update();
    p.handleEdges(false); // predators bounce

    // check collisions with boids (reverse loop on flock)
    for (let j = flock.length - 1; j >= 0; j--) {
      let b = flock[j];
      let d = p5.Vector.dist(p.position, b.position);
      if (d <= PREDATOR_EAT_RADIUS) {
        // comprobar cooldown
        let nowSec = millis() / 1000.0;
        if ((nowSec - (p.lastEat || -Infinity)) >= PREDATOR_EAT_COOLDOWN) {
          // permitir comer
          p.lastEat = nowSec;
          // spawn predator ring at predator world position
          let ringHue = (p.hue + map(bass,0,255,-40,40) + 360) % 360;
          let ringCol = color(ringHue, 95, 70);
          let startR = 8 + random(4, 14);
          predatorRings.push(new PredatorRing(p.position, startR, ringCol));
          // optional: spawn a subtle wave too (screen coords)
          let screenP = worldToScreen(p.position);
          waves.push(new Wave(screenP.x, screenP.y, color(ringHue, 95, 70)));
          // remove the boid (comido)
          flock.splice(j, 1);
          // break para evitar que el mismo depredador intente comerse múltiples boids en la misma iteración
          break;
        }
      }
    }
  }

  // update & draw predatorRings
  for (let i = predatorRings.length - 1; i >= 0; i--) {
    predatorRings[i].update();
    predatorRings[i].display();
    if (predatorRings[i].isDead()) predatorRings.splice(i, 1);
  }

  // draw boids & predators
  let isFlowDominantVisual = flowInfluence > 0.6;
  for (let b of flock) b.draw(isFlowDominantVisual);
  for (let p of predators) p.draw();

  // draw mouse-depredador
  if (mousePredatorActive) {
    push();
    let mw = screenToWorld(mouseX, mouseY);
    let screenPos = worldToScreen(mw);
    push();
    translate(screenPos.x, screenPos.y);
    noStroke();
    fill(12, 90, 80);
    let size = max(6, 14 / currentZoom);
    beginShape();
    vertex(size, 0);
    vertex(-size / 1.5, size / 1.5);
    vertex(-size / 1.5, -size / 1.5);
    endShape(CLOSE);
    pop();
    pop();
  }

  if (showFlowVectors && (elapsed <= FLOW_PHASE_END || elapsed < (FLOCK_START + TRANSITION_SECONDS))) flowField.drawVectors();

  // HUD bars
  push();
  noStroke();
  fill(0,0,100,10);
  rect(8, height - 40, map(bass,0,255,0,160), 8);
  rect(8, height - 24, map(treble,0,255,0,160), 8);
  pop();

  // portals, waves cleanup
  for (let i = portals.length - 1; i >= 0; i--) { portals[i].update(); portals[i].display(); if (portals[i].isDead()) portals.splice(i,1); }
  for (let i = waves.length - 1; i >= 0; i--) { waves[i].update(); waves[i].display(); if (waves[i].isDead()) waves.splice(i,1); }

  if (glow && millis() - glowStart > glowDuration) glow = false;

  drawControlsHUD();

  push();
  fill(0,0,100,180);
  textSize(12);
  textAlign(RIGHT, TOP);
  text("t: " + nf(elapsed, 2, 2) + "s", width - 10, 10);
  pop();
}

function spawnPredator() {
  if (predators.length >= PREDATOR_MAX) return;
  let px = random(cameraCenterWorld.x - 120, cameraCenterWorld.x + 120);
  let py = random(cameraCenterWorld.y - 120, cameraCenterWorld.y + 120);
  const shapes = ["triangle","square","pentagon","star","hexagon"];
  let st = shapes[predators.length % shapes.length];
  let p = new Predator(px, py, st);
  predators.push(p);
}

function mousePressed() {
  if (mouseButton === LEFT) { glow = true; glowStart = millis(); }
  else if (mouseButton === RIGHT) { portals.push(new PortalPulse(mouseX, mouseY)); waves.push(new Wave(mouseX, mouseY, color(map(treble,0,255,180,300),70,90))); }
}

function drawControlsHUD() {
  push();
  rectMode(CORNER);
  noStroke();
  fill(0,0,100,10);
  rect(10,10,340,85,8);
  fill(0,0,100); textSize(13); textAlign(LEFT, TOP); text("Controles:", 18, 14);
  textSize(12); fill(0,0,100,220);
  text("Espacio: Play | P: Pausa | M: cambiar paleta | S: Pantallazo", 18, 34);
  text("I: Invertir FlowField | V: mostrar/ocultar FlowField", 18, 52);
  text("Clic Izq: Glow | Clic Der: Portal", 18, 70);
  pop();
}

```

## Captura de pantalla representativa
<img width="1920" height="1440" alt="generative_zoom_boids (4)" src="https://github.com/user-attachments/assets/07f50cc8-65bf-48fa-9f5f-25df228a6cc1" />

## Autoevaluación:
__Mi nota es:__ __5,0__. Porque cumplí con todas las actividades de forma satisfactoria. Desde las obras de interés, la investigación autónoma, las experimentaciones en Flow Fields y Flocking, hasta un trabajo cuidadoso en el Apply.
