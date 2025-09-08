# Evidencias de la unidad 4

## Explicación conceptual de la obra

* ¿Qué concepto de la unidad 4 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
El concepto central es en base a los __péndulos__. Construí tres doble péndulos que comparten un mismo origen, pero cada uno tiene características físicas diferenciadoras y responden a funciones diferentes con respecto a la música.

>- __Péndulo #1:__ corto, morado oscuro, influenciado por los __altos__.
>- __Péndulo #2:__ mediano, naranja, influenciado por el __volumen__.
>- __Péndulo #3:__ largo, azul oscuro, influenciado por los __bajos__.

>Cada péndulo tiene límites en sus velocidades para evitar __loops de circulos__, __bugs en su comportamiento__ o __poca variabilidad__. Además, para equilibrar la relación entre música y movimiento físico, agregué un __intervalo de 3 segundos en la lectura de bajos, altos y volumen__. Esto evita que las variaciones musicales generen un movimiento demasiado caótico o no deje apreciar la naturalidad de la física, manteniendo un balance entre el modelo del péndulo y la influencia de la música aplicada.

* ¿Qué concepto de la unidad 3 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Apliqué el __LerpColor__, haciendo que el __color del trazo__ de cada péndulo __cambie su intensidad según la velocidad angular__. Cuando el movimiento es rápido (normalizado a 1), los colores se vuelven más claros. En cambio, cuando el movimiento se ralentiza (normalizado a 0), los colores se tornan a unos tonos más oscuros.

* ¿Qué concepto de la unidad 2 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> La __fricción__ se encuentra de forma __intrínseca en la física del péndulo__. Esta depende de la velocidad en cada frame: cuanto más rápido se mueven, mayor es la pérdida de energía, lo que hace que progresivamente vayan perdiendo fuerza de manera natural.

* ¿Qué concepto de la unidad 1 y cómo lo aplicaste en la obra?
> Tu respuesta aquí:
> Incorporé un __Lévy Flight en el origen de los péndulos__, lo que añade un grado de aleatoriedad a su movimiento. Este origen no es fijo, sino que combina la aleatoriedad con la __influencia del volumen__ de la música y la __atracción del mouse__.

## ¿Cómo resolviste la interacción?
> Tu respuesta aquí:
> La interacción se da principalmente con __el mouse__, que ejerce una __fuerza de atracción sobre el origen de los péndulos__. Según la posición del mouse en el Canvas, el origen se desplaza, generando variaciones adicionales en los trazos. Esa influencia no es igual en los dos ejes: en el eje X la fuerza está amplificada (*100), mientras que en el eje Y es más moderada (*50).

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra](https://editor.p5js.org/JuanJAreiza/sketches/rfzGNqb4c)

## Código de la obra 

``` js
let pendulums = [];
let g = 1; // gravedad

let song;
let fft;
let amplitude;

let lastMusicInfluenceTime = 0;
let musicInfluenceInterval = 3000; // cada 3s meto un empujón musical

let commonX; // origen X de todos los péndulos
let commonY; // origen Y de todos los péndulos

// origen X de todos los péndulos
let levyX = 0;
let levyY = 0;
let levyLambda = 1.5; // controla la distribución de Lévy (1-2)
let levyScale = 5;   // tamaño de los pasos

// Atracción del mouse
let mouseAttractionStrength = 0.02;
let mouseAttractionRadius = 150;


function preload() {
  song = loadSound('Hoppipolla.mp3'); 
}

function setup() {
  createCanvas(800, 800);
  angleMode(RADIANS); // 

  fft = new p5.FFT();
  amplitude = new p5.Amplitude();

// arranco el origen en el medio
  commonX = width / 2;
  commonY = height / 4; 

  levyX = commonX;
  levyY = commonY;

// Péndulo 1 (Corto, Morado Oscuro, Influencia de Altos)
  let purpleBase = color(75, 0, 130);
  let purpleSlow = color(purpleBase, 70);
  let purpleFast = color(255, 0, 255, 200);
  pendulums.push(new DoublePendulum(
    commonX, 
    commonY, 
    100,     
    100,     
    10,      
    10,      
    PI / 2 + 0.1, 
    PI / 2 + 0.2, 
    purpleBase, 
    purpleSlow,
    purpleFast,
    'highs'
  ));

  // Péndulo 2 (Mediano, Naranja, Influencia de Volumen)
  let orangeBase = color(255, 165, 0);
  let orangeSlow = color(orangeBase, 70);
  let orangeFast = color(255, 255, 0, 200);
  pendulums.push(new DoublePendulum(
    commonX, 
    commonY, 
    150,     
    100,     
    10,      
    10,      
    PI / 2 - 0.1, 
    PI / 2 - 0.2, 
    orangeBase, 
    orangeSlow,
    orangeFast,
    'volume'
  ));

  // Péndulo 3 (Largo, Azul Oscuro, Influencia de Bajos)
  let blueBase = color(0, 0, 139);
  let blueSlow = color(blueBase, 70);
  let blueFast = color(0, 255, 255, 200);
  pendulums.push(new DoublePendulum(
    commonX, 
    commonY, 
    200,     
    100,     
    10,      
    10,      
    PI / 2,  
    PI / 2,  
    blueBase, 
    blueSlow,
    blueFast,
    'lows'
  ));

  pendulums.forEach(p => {
    p.buffer = createGraphics(width, height);
    p.buffer.background(0, 0);
    p.buffer.strokeWeight(1);
  });

  song.play();
  lastMusicInfluenceTime = millis(); 
}

function draw() {
  background(0);

  // movimiento loco del origen con Lévy
  let levyStep = 0;
  levyStep = constrain(pow(random(0, 1), -1.0 / levyLambda) * levyScale, 0, width / 8); 
  let levyAngle = random(TWO_PI); 

  levyX += levyStep * cos(levyAngle);
  levyY += levyStep * sin(levyAngle);

  levyX = constrain(levyX, width * 0.1, width * 0.9);
  levyY = constrain(levyY, height * 0.1, height * 0.6); 

  // obtengo el volumen actual para influir en commonY
  let vol = amplitude.getLevel();

 // atracción del mouse al origen
  let mouseForceX = 0;
  let mouseForceY = 0;
  let distToMouse = dist(commonX, commonY, mouseX, mouseY);


  if (distToMouse < mouseAttractionRadius && distToMouse > 0) { 
    let dirX = mouseX - commonX;
    let dirY = mouseY - commonY;
    
    let dirMag = sqrt(dirX*dirX + dirY*dirY);
    dirX /= dirMag;
    dirY /= dirMag;

    let attraction = map(distToMouse, 0, mouseAttractionRadius, mouseAttractionStrength, 0);
    
    mouseForceX = dirX * attraction;
    mouseForceY = dirY * attraction;
  }

  // actualizo el origen combinando todo
  commonX = levyX;
  commonX += mouseForceX * 100;

  let volumeInfluenceY = map(vol, 0, 1, height * 0.1, height * 0.4); 
  commonY = lerp(levyY, volumeInfluenceY, 0.5); 
  commonY += mouseForceY * 50;

  commonX = constrain(commonX, width * 0.1, width * 0.9);
  commonY = constrain(commonY, height * 0.1, height * 0.6); 


  pendulums.forEach(p => {
    p.cx = commonX;
    p.cy = commonY;
  });


  let applyMusicInfluence = false;
  
  if (millis() - lastMusicInfluenceTime > musicInfluenceInterval) {
    applyMusicInfluence = true;
    lastMusicInfluenceTime = millis();
  }

  let bassInfluence = 0;
  let trebleInfluence = 0;
  let volumeInfluenceAcc = 0; 

  if (applyMusicInfluence) {
    let spectrum = fft.analyze();
    let bass = fft.getEnergy("bass");
    let treble = fft.getEnergy("treble");

    bassInfluence = map(bass, 0, 255, 0, 0.05); 
    trebleInfluence = map(treble, 0, 255, 0, 0.05); 
    volumeInfluenceAcc = map(vol, 0, 1, 0, 0.1); 
  }

  for (let i = 0; i < pendulums.length; i++) {
    let p = pendulums[i];

    if (applyMusicInfluence) {
      if (p.influence === 'highs') {
        p.audio_acc_a1 = trebleInfluence; 
      } else if (p.influence === 'volume') {
        p.audio_acc_a2 = volumeInfluenceAcc;
      } else if (p.influence === 'lows') {
        p.audio_acc_a1 = bassInfluence;
      }
    } else {
      p.audio_acc_a1 = 0; 
      p.audio_acc_a2 = 0;
    }

    p.update();
    p.draw();
  }
}


class DoublePendulum {
  constructor(cx, cy, r1, r2, m1, m2, a1, a2, colorP, strokeColorSlow, strokeColorFast, influence) {
    this.cx = cx; 
    this.cy = cy; 
    this.r1 = r1;
    this.r2 = r2;
    this.m1 = m1;
    this.m2 = m2;
    this.a1 = a1; 
    this.a2 = a2; 
    this.a1_v = 0; 
    this.a2_v = 0; 
    this.colorP = colorP;
    this.strokeColorSlow = strokeColorSlow;
    this.strokeColorFast = strokeColorFast;
    this.influence = influence;

    this.px2 = -1; 
    this.py2 = -1; 
    this.buffer;

    this.max_a_v = 0.5;
    
    this.audio_acc_a1 = 0;
    this.audio_acc_a2 = 0;
  }

  update() {
    let num1 = -g * (2 * this.m1 + this.m2) * sin(this.a1);
    let num2 = -this.m2 * g * sin(this.a1 - 2 * this.a2);
    let num3 = -2 * sin(this.a1 - this.a2) * this.m2;
    let num4 = this.a2_v * this.a2_v * this.r2 + this.a1_v * this.a1_v * this.r1 * cos(this.a1 - this.a2);
    let den = this.r1 * (2 * this.m1 + this.m2 - this.m2 * cos(2 * this.a1 - 2 * this.a2));
    let a1_a = (num1 + num2 + num3 * num4) / den;

    num1 = 2 * sin(this.a1 - this.a2);
    num2 = (this.a1_v * this.a1_v * this.r1 * (this.m1 + this.m2));
    num3 = g * (this.m1 + this.m2) * cos(this.a1);
    num4 = this.a2_v * this.a2_v * this.r2 * this.m2 * cos(this.a1 - this.a2);
    den = this.r2 * (2 * this.m1 + this.m2 - this.m2 * cos(2 * this.a1 - 2 * this.a2));
    let a2_a = (num1 * (num2 + num3 + num4)) / den;

    a1_a += this.audio_acc_a1;
    a2_a += this.audio_acc_a2;

    this.a1_v += a1_a;
    this.a2_v += a2_a;
    
    // fricción
    let frictionFactor1 = map(abs(this.a1_v), 0, this.max_a_v, 0.999, 0.98); 
    let frictionFactor2 = map(abs(this.a2_v), 0, this.max_a_v, 0.999, 0.98); 
    
    this.a1_v *= frictionFactor1;
    this.a2_v *= frictionFactor2;

    this.a1_v = constrain(this.a1_v, -this.max_a_v, this.max_a_v);
    this.a2_v = constrain(this.a2_v, -this.max_a_v, this.max_a_v);

    this.a1 += this.a1_v;
    this.a2 += this.a2_v;
  }

  draw() {
    let x1_rel = this.r1 * sin(this.a1);
    let y1_rel = this.r1 * cos(this.a1);

    let x2_rel = x1_rel + this.r2 * sin(this.a2);
    let y2_rel = y1_rel + this.r2 * cos(this.a2);

    push();
    translate(this.cx, this.cy); 

    stroke(this.colorP);
    strokeWeight(2);

    line(0, 0, x1_rel, y1_rel);
    fill(this.colorP);
    ellipse(x1_rel, y1_rel, this.m1 * 2, this.m1 * 2); 

    line(x1_rel, y1_rel, x2_rel, y2_rel);
    fill(this.colorP);
    ellipse(x2_rel, y2_rel, this.m2 * 2, this.m2 * 2);

    pop(); 

    this.buffer.push();
    this.buffer.translate(this.cx, this.cy); 
    if (this.px2 != -1) {
      // Calcular la magnitud de la velocidad angular combinada
      // Normalizo valor entre 0 y 1, donde 0 es muy lento y 1 es la velocidad máxima.
      let combinedSpeed = abs(this.a1_v) + abs(this.a2_v);
      let normalizedSpeed = map(combinedSpeed, 0, this.max_a_v * 0.2, 0, 1);
      normalizedSpeed = constrain(normalizedSpeed, 0, 1);


      let currentStrokeColor = lerpColor(this.strokeColorSlow, this.strokeColorFast, normalizedSpeed);
      
      this.buffer.stroke(currentStrokeColor); 
      this.buffer.line(this.px2, this.py2, x2_rel, y2_rel);
    }
    this.px2 = x2_rel;
    this.py2 = y2_rel;
    this.buffer.pop();

    image(this.buffer, 0, 0);
  }
}

function keyPressed() {
 if (key === 'S' || key === 's') saveCanvas('obraUnidad4', 'jpg');
}
```

## Captura de pantalla representativa
![obraUnidad4](https://github.com/user-attachments/assets/b1006b00-0226-4bc3-befd-c7edc306e37a)








