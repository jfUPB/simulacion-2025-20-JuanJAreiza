# Evidencias de la unidad 7

## Actividades

* __Actividad 1.__

> * __1.__ De todos los ejemplos, los que más me llamaron la atención fueron:

> __Inflación (Inflation):__ Me parece muy ingeniono la interpretación del concepto del aumento de precios, representando la unidad monetaria en las Os que contiene la palabra y que cada vez son más, del mismo modo que funciona la inflación.

> <img width="596" height="59" alt="image" src="https://github.com/user-attachments/assets/1e782c32-17e7-47c9-916b-db624bbe3602" />

> __Luna (Moon):__ En este caso hay una marcada diferencia de tamaño entre las dos Os que componen la palabra, una mucho más pequeña con respecto a las demás letras. Además, se siente una ligera orbitación de esta con respecto a la primera O que se encuentra en la palabra. Todo esto para dar una pequeña y rápida sensación de simulación de la luna.

> <img width="368" height="165" alt="image" src="https://github.com/user-attachments/assets/94abbbf4-9830-42de-9838-d04b75c6f9f0" />

> __Paralelo (Parallel):__ Esta es una de las imágenes que más estética me ha parecido. Siento que el uso de las Ls, aprovechando que son verticales y tan cercanas, permite dar a comprensión clara el concepto del paralelismo matemático.

> <img width="451" height="223" alt="image" src="https://github.com/user-attachments/assets/67f93da3-addb-456d-a092-e8134f12c898" />

> __Enfermedad (Ill):__ Una de las más iconografícas sin querer por la misma naturalidad de la palabra. Simplemente rotarla y animar la i (adicional al sonido) es suficiente para entender lo que me quieren contar, no obstante encontrar la palabra textual la primera vista -para alguien que no tiene contexto-, puede ser interesante.

> <img width="366" height="221" alt="image" src="https://github.com/user-attachments/assets/81860831-ae0f-493c-9b82-1d5817288d49" />

> * __2.__ Mis propias ideas:

> __Procastinación:__ Esta fue de las primeras palabas que se me ocurrieron. Me imaginé en primera instancia un __timer__ (visual o auditivo) que muestre en cuanto tiempo se va a acabar la animación. Luego la palabra se irá escribiendo poco a poco, pero por cada letra que pasa (aprovechando que es una palabra larga), van apareciendo más lentamente hasta que ya no sale; incluso de devuelve para revisar las otras letras. También las últimas letras que se hayan escrito salen a caminar o se distraen con cualquier cosa, sale del Canvas y luego vuelve. Justo antes de acabar el __timer__, todas las letras se dan cuenta y comienzan a organizarce; volver a sus puestos para poder terminar la palabra a última hora.

> __Fascismo:__ Lo político no descansa, por ende, hablar de fascismo en este momento por medio de una palabra que se abstrae para conseguir una esvástica nazi es más que idóneo. Sobretodo si luego la intención es pintarla con los colores de cierto país de Norte América.


* __Actividad 2.__

> Recursos de demos que me llamaron la atención: Time Scaling, Sprites, Sensors, Gyroscope, Composite Manipulation, 

#### Experimentos:

> * __Experimento 1:__
<img width="1001" height="748" alt="image" src="https://github.com/user-attachments/assets/51271b54-70bf-45bb-a08a-1f66b0db3f22" />

> [Mi experimento 1 | GIF](https://jumpshare.com/s/IuL4qzIbzKhG2AacVZ2x)

> * __Experimento 2:__
<img width="1003" height="754" alt="image" src="https://github.com/user-attachments/assets/d65047e2-a614-49cd-b08e-6aa8f1061b62" />

> [Mi experimento 2 | GIF](https://jumpshare.com/s/57Oq8Jjv34FQAtFMmkW5)

#### Conceptos:
> * __Engine:__ Es el motor físico principal de Matter.js. Se encarga de calcular todas las fuerzas, colisiones, aceleraciones y movimientos dentro del mundo.

> * __World:__ Es el contenedor donde existen todos los objetos físicos (cuerpos, restricciones, etc.). Los Bodies y Constraints deben agregarse al World para que el motor los procese.

> * __Bodies:__ Representan los objetos físicos del mundo. Desde formas simples (rectángulos, círculos, polígonos) a complejas, y tienen las mismas propiedades físicas que hemos trabajado: masa, fricción, restitución, densidad, etc.

> * __Constraint:__ Es una unión entre dos cuerpos. Nos permite conectar 2 o más bodies con simulaciones de resortes, cuerdas o bisagras.

> * __MouseConstraint:__ Permite interactuar con los cuerpos usando el mouse: arrastrarlos, empujarlos, etc.
 
> __Dificultades que experimenté:__ Al configurar Matter.js por primera vez, una de las principales dificultades fue entender la diferencia entre los módulos (Engine, World, Render, Runner) y cómo deben inicializarse y conectarse correctamente. Además el agregar su biblioteca al HTML me generó errores inicialmente.

## Apply

> __1. Palabra elegida__
**Ansiedad**

---

> __2. Idea conceptual__

> El objetivo fue representar de manera visual y táctil la experiencia de la ansiedad. Cada letra funciona como un __pensamiento intrusivo__, que aparece de forma impredecible, a veces de forma violenta y a veces con suavidad, chocando contras las demás letras, simbolizando __cómo los pensamientos ansiosos pueden colisionar y superponerse en la mente__.

> A medida que la animación progresa, las letras tiemblan, saltan y giran, evocando la __tensión muscular__, la __falta de respiración__ y la sensación de __bloqueo__ que acompañan a la ansiedad. En los momentos de mayor intensidad, el caos físico refleja la __incapacidad de moverse y el miedo__ (complejidad para interactuar con las letras) que se experimenta internamente. Además, __los sentidos se agudizan__, todos los sonidos y colores se sienten más e incluso se distorsionan.

> Finalmente, cuando se introduce un control progresivo del movimiento y la estabilización de las letras, la "animación" muestra cómo la __respiración consciente y la regulación física__ pueden aliviar los síntomas de la ansiedad, restaurando un estado de calma y control mental.

---

__3. Aspectos técnicos clave__

### Formación de las letras
- Cada letra de la palabra "Ansiedad" se representa con un __cuerpo rígido (rectangle)__ de Matter.js.
- Las letras se colocan inicialmente en posiciones ancladas en el centro del lienzo y __se lanzan con un pequeño desplazamiento aleatorio__ para generar dinamismo.
- Cada letra tiene un __constraint tipo resorte__ que la conecta a su posición de anclaje, permitiendo que rebote y oscile de manera física, __simulando la tensión muscular y el temblor__.

### Propiedades físicas importantes
- __Fricción y restitución:__ ajustadas para que las letras colisionen de forma violenta, pero sin perder la sensación de rebote controlado.
- __Fuerzas laterales y verticales aleatorias:__ generan movimientos impredecibles, simbolizando pensamientos intrusivos y espasmos musculares.
- __Masa y gravedad:__ para reforzar la sensación de peso y tensión en cada letra.
- __Angular velocity:__ pequeñas rotaciones aleatorias que refuerzan la sensación de inestabilidad.

### Uso de restricciones
- Los __constraints (resortes)__ mantienen cada letra conectada a su posición base, permitiendo que vuelva a su lugar tras los impulsos, lo que representa la recuperación progresiva de control sobre la ansiedad.
- En la fase final, se aumenta la rigidez de los constraints para simbolizar la __regulación de la respiración y el retorno de calma__.
- Durante el colapso, se eliminan los constraints para mostrar cómo los pensamientos caen al poder recuperar el control de nuestro propio cuerpo con una regulación consciente (actua la gravedad del sistema).

---


## Enlace a la obra en el editor de p5.js

[Aquí está mi obra](https://editor.p5js.org/JuanJAreiza/sketches/RUwt509mD)

## Código de la obra 

``` js
/* ===================== CONSTANTES AJUSTABLES ===================== */
let TOTAL_TIME = 25;
let SPAWN_INTERVAL = 0.5;
let FINAL_PHASE_PERCENTAGE = 0.10;

let CANVAS_W = 800, CANVAS_H = 600;
let GRAVITY = 0.9;
let LETTER_RESTITUTION = 0.6;
let LETTER_FRICTION = 0.2;
let SPRING_STIFFNESS = 0.01;
let SPRING_DAMPING = 0.08;
let LATERAL_FORCE_MAG = 0.0006;
let LAST_DISTRACT_COUNT = 3;

let AUDIO_FILE = 'time.mp3';
let MAX_AUDIO_RATE = 2.2;
let ENABLE_AUDIO_RAMP = true;

let firstSpawnTriggered = false;

let collapseHUDUpdated = false;

let TEXT = "Ansiedad";
let textSizeBase = 48;

/* ===================== VARIABLES GLOBALES ===================== */
let engine, world;
let letters = [];
let started = false;
let startTime = 0;
let lastSpawnAt = 0;
let spawnIndex = 0;
let finalPhaseStarted = false;
let canvasElement;

let audioEnded = false;
let postSpawnDelay = 1200;
let lastAllSpawnedAt = null;

let timeAudio = null;
let heartAudio = null;
let heartAudioStarted = false;

let bgPulsePhase = 0;

// ----- Variables del fondo (usar p5.Color) -----
let currentBG = null;         // color actual (p5.Color)
let targetColor = null;       // color objetivo (p5.Color)
let lastBGChange = 0;         // timestamp última actualización
let finalTransitionStart = null;
let collapseColor = null;
let finalBlue = null;         // color azul final (se asigna en setup si quieres)

// 🔧 Se declaran antes de usarlas
let EngineM, WorldM, BodiesM, BodyM, ConstraintM, MouseM, MouseConstraintM, CompositeM, VerticesM;
let MATTER_LOADED = false;
let mouseConstraintGlobal = null;
let collapseSound = null;
let collapseStarted = false;
let collapseDelay = 3000;
let finalCollapseTriggered = false;
let collapseTriggered = false;
let collapseStartTime = 0;

/* ===================== preload ===================== */
function preload() {
  timeAudio = loadSound('time.mp3');      // audio principal
  heartAudio = loadSound('cora.mp3');     // latido del corazón
  collapseSound = loadSound('respira.mp3');
}

/* ===================== setup ===================== */
function setup() {
  // Inicializar el color correctamente aquí
  currentBG = color(0);

  let infoDiv = document.getElementById('info');
  if (infoDiv) infoDiv.style.display = 'none';

  canvasElement = createCanvas(CANVAS_W, CANVAS_H);
  canvasElement.parent(document.body);
  textSize(textSizeBase);
  textAlign(CENTER, CENTER);
  noStroke();

  prepareLetterAnchors();
  lastSpawnAt = millis() - SPAWN_INTERVAL * 1000;

  if (window.Matter) {
    loadMatterAliasesAndInit();
  } else {
    loadMatterJS(() => loadMatterAliasesAndInit());
  }

  window.addEventListener('keydown', (e) => {
    if (e.code === 'Space' || e.keyCode === 32) {
      e.preventDefault();
      startOrRestart();
    }
  });

  console.log('Setup listo. Presiona Espacio para iniciar.');
}

/* ===================== carga dinámica Matter.js ===================== */
function loadMatterJS(callback) {
  if (window.Matter) { MATTER_LOADED = true; callback(); return; }
  let s = document.createElement('script');
  s.src = 'https://cdnjs.cloudflare.com/ajax/libs/matter-js/0.19.0/matter.min.js';
  s.onload = function() { MATTER_LOADED = true; callback(); };
  s.onerror = function() { console.error('No se pudo cargar Matter.js'); };
  document.head.appendChild(s);
}

/* ===================== init Matter aliases y world ===================== */
function loadMatterAliasesAndInit() {
  // ✅ Estas variables ya están declaradas arriba (antes de setup)
  EngineM = Matter.Engine;
  WorldM = Matter.World;
  BodiesM = Matter.Bodies;
  BodyM = Matter.Body;
  ConstraintM = Matter.Constraint;
  MouseM = Matter.Mouse;
  MouseConstraintM = Matter.MouseConstraint;
  CompositeM = Matter.Composite;
  VerticesM = Matter.Vertices;

  engine = EngineM.create();
  world = engine.world;
  engine.gravity.y = GRAVITY;

  // Suelo estático real
  // Suelo estático real
  let ground = BodiesM.rectangle(CANVAS_W / 2, CANVAS_H - 18, CANVAS_W, 36, { isStatic: true, friction: 1 });
  WorldM.add(world, ground);

  // ✅ Agregar muros para que las letras no se salgan
  createCanvasWalls();


  let mm = MouseM.create(canvasElement.elt);
  mm.pixelRatio = pixelDensity();
  mouseConstraintGlobal = MouseConstraintM.create(engine, { 
    mouse: mm, 
    constraint: { stiffness: 0.2, render: { visible: false } }
  });
  WorldM.add(world, mouseConstraintGlobal);

  MATTER_LOADED = true;
  console.log('Matter inicializado.');
}

/* ===================== preparar anchors ===================== */
function prepareLetterAnchors() {
  textSize(textSizeBase);
  let widths = [];
  let totalWidth = 0;
  for (let i = 0; i < TEXT.length; i++) {
    let w = textWidth(TEXT[i]) + 12;
    widths.push(w);
    totalWidth += w;
  }
  let baseX = CANVAS_W / 2 - totalWidth / 2;
  let baseY = CANVAS_H / 2;
  letters = [];
  let x = baseX;
  for (let i = 0; i < TEXT.length; i++) {
    letters.push({
      body: null,
      char: TEXT[i],
      anchor: { x: x + widths[i]/2, y: baseY },
      size: { w: widths[i], h: textSizeBase + 10 },
      constraint: null,
      hidden: true,
      spawnTime: null,
      desiredFriction: LETTER_FRICTION
    });
    x += widths[i];
  }
}

/* ===================== fondo dinámico ===================== */
/* ===================== fondo dinámico (reemplazo) ===================== */
function updateBackgroundDynamic() {
  // Asegurarnos de tener p5 colors definidos
  if (!currentBG) currentBG = color(20, 20, 35);   // color inicial suave
  if (!targetColor) targetColor = currentBG;
  if (!finalBlue) finalBlue = color(60, 90, 200);  // azul sereno final

  // calcular elapsed (segundos) — si no iniciado, 0
  let elapsed = (started && startTime) ? (millis() - startTime) / 1000 : 0;

  // 1) Si pasamos de 35s -> iniciar transición lenta al azul final
  if (elapsed >= 35) {
    if (!finalTransitionStart) finalTransitionStart = millis();
    // t de 0..1 en 3 segundos
    let t = constrain((millis() - finalTransitionStart) / 3000, 0, 1);
    currentBG = lerpColor(currentBG, finalBlue, t * 0.06 + 0.02); // lerp algo más suave
    background(currentBG);
    return;
  }

  // 2) Antes de 10s -> colores suaves y transiciones lentas
  if (elapsed < 10) {
    // cada 2.5s cambiar objetivo
    if (millis() - lastBGChange > 2500) {
      lastBGChange = millis();
      targetColor = random([
        color(180, 200, 255), // azul suave
        color(220, 180, 255), // lila
        color(255, 200, 230), // rosa pastel
        color(200, 220, 255), // celeste
        color(245, 210, 255)  // violeta suave
      ]);
    }
    // transición muy lenta
    currentBG = lerpColor(currentBG, targetColor, 0.01);
    background(currentBG);
    return;
  }

  // 3) Entre 10s y TOTAL_TIME: ir incrementando caos (más cambios, más grises)
  if (elapsed >= 10 && elapsed <= TOTAL_TIME) {
    // normalizar progreso entre 10 y TOTAL_TIME -> 0..1
    let tfrac = (elapsed - 10) / max(0.001, (TOTAL_TIME - 10));
    tfrac = constrain(tfrac, 0, 1);

    // Probabilidades: pastel disminuye, grises aumentan
    let pastelProb = 1 - tfrac;  // va de 1 a 0
    let darkProb = tfrac;        // va de 0 a 1

    // Intervalo de cambio se reduce con el tiempo (de lento a rápido)
    let changeInterval = lerp(2500, 180, tfrac);
    if (millis() - lastBGChange > changeInterval) {
      lastBGChange = millis();
      if (random() < pastelProb) {
        // elegir color suave ligeramente randomizado
        targetColor = color(
          random(150, 255),
          random(130, 220),
          random(170, 255)
        );
      } else {
        // color oscuro / gris según avance
        let g = floor(lerp(160, 30, tfrac));
        // añadir pequeña variación
        targetColor = color(g + random(-10, 10), g + random(-10, 10), g + random(-10, 10));
      }
    }

    // velocidad de interpolación hacia target crece con tfrac para cambios más bruscos
    let interp = lerp(0.02, 0.18, tfrac);
    currentBG = lerpColor(currentBG, targetColor, interp);
    background(currentBG);
    return;
  }

  // 4) Si elapsed > TOTAL_TIME y < 35: seguir volviéndose más inestable/oscuro
  if (elapsed > TOTAL_TIME && elapsed < 35) {
    // cambios rápidos hacia grises/negros
    if (millis() - lastBGChange > 180) {
      lastBGChange = millis();
      let g = random(10, 90);
      targetColor = color(g, g, g);
    }
    currentBG = lerpColor(currentBG, targetColor, 0.18);
    background(currentBG);
    return;
  }

  // Fallback: dibujar color actual
  background(currentBG);
}


/* ===================== draw (loop) ===================== */
function draw() {
  // 🎨 Fondo dinámico
  updateBackgroundDynamic();

  // 🔮 Efecto visual de colapso (ligera cámara lenta/reverberación)
  if (finalCollapseTriggered && collapseTriggered) {
    push();
    // Oscurecer ligeramente y desenfocar/duplicar para efecto reverberación
    fill(0, 0, 20, 30); 
    rect(0, 0, CANVAS_W, CANVAS_H);
    scale(0.995); // leve cámara lenta visual
    pop();
  }

  // HUD
  drawHUD_simplified();

  if (!MATTER_LOADED) {
    fill(255);
    textSize(16);
    textAlign(CENTER, CENTER);
    text('Cargando Matter.js...', CANVAS_W / 2, CANVAS_H / 2);
    return;
  }

  if (engine && typeof EngineM !== 'undefined' && EngineM) {
    EngineM.update(engine, 1000 / 60);
  }

  let elapsed = 0;
  if (started && startTime) {
    elapsed = (millis() - startTime) / 1000;
  }

  if (started && !heartAudioStarted && elapsed >= 20) {
  if (heartAudio && typeof heartAudio.isLoaded === 'function' && heartAudio.isLoaded()) {
    heartAudio.play();
    heartAudioStarted = true;
    console.log('❤️ heartAudio iniciado a los 20s');
  }
}

  
  if (started) {
    // 🎵 Control del audio principal
    if (timeAudio && typeof timeAudio.isLoaded === 'function' && timeAudio.isLoaded()) {
      // 🕒 Ajuste de velocidad dinámica
    if (ENABLE_AUDIO_RAMP && !finalPhaseStarted && elapsed > 5) {
  // Mapear desde 5s hasta TOTAL_TIME
  let tfrac = constrain((elapsed - 5) / (TOTAL_TIME - 5), 0, 1);
  const MAX_AUDIO_RATE_FINAL = 4.0; 
  let targetRate = 1 + tfrac * (MAX_AUDIO_RATE_FINAL - 1);
  try { timeAudio.rate(targetRate); } catch(e) {}
} else if (ENABLE_AUDIO_RAMP && elapsed <= 5) {
  // Mantener velocidad normal los primeros 5s
  try { timeAudio.rate(1); } catch(e) {}
}

    }

    // 🌀 Spawn de letras
    const totalLetters = letters.length;
    const START_DELAY = 2;
    const MARGIN_TIME = 1.5;
    const effectiveTime = max(0, TOTAL_TIME - START_DELAY - MARGIN_TIME);
    const baseInterval = effectiveTime > 0 ? effectiveTime / max(1, totalLetters) : SPAWN_INTERVAL;

    if (elapsed >= START_DELAY && spawnIndex < totalLetters) {
      let elapsedSinceLast = (millis() - lastSpawnAt) / 1000;
      let accelFactor = map(spawnIndex, 0, totalLetters - 1, 1.8, 0.6);
      let currentInterval = baseInterval * accelFactor;

      if (spawnIndex === 0 && !firstSpawnTriggered) {
        let lt = spawnLetter(spawnIndex);
        if (lt && lt.body) { lt.body.restitution = 0.8; lt.body.friction = 0.05; }
        spawnIndex++; lastSpawnAt = millis(); firstSpawnTriggered = true;
      } else if (elapsedSinceLast >= currentInterval) {
        let lt = spawnLetter(spawnIndex);
        if (lt && lt.body) {
          let slowdownFactor = map(spawnIndex, 0, totalLetters - 1, 0, 1);
          lt.body.friction = 0.1 + slowdownFactor * 0.6;
          lt.body.restitution = 0.7 - slowdownFactor * 0.5;
        }
        spawnIndex++; lastSpawnAt = millis();
        if (spawnIndex === totalLetters) lastAllSpawnedAt = millis();
      }
    } else if (spawnIndex >= totalLetters && lastAllSpawnedAt && millis() - lastAllSpawnedAt >= postSpawnDelay) {
      finalizeWord();
      lastAllSpawnedAt = null;
    }

    // 🕓 Fase final y distracciones
    let tfrac = constrain(elapsed / TOTAL_TIME, 0, 1);
    if (!finalPhaseStarted && tfrac >= 1 - FINAL_PHASE_PERCENTAGE) enterFinalPhase();
    else if (!finalPhaseStarted && !finalCollapseTriggered) applyDistractionToAllLettersProgressive();

    // 💥 Fuerzas exponenciales
    let intensity = pow(1.15, tfrac * 10);
    let forceMagnitude = LATERAL_FORCE_MAG * intensity;

    if (!finalCollapseTriggered) {
      for (let lt of letters) {
        if (!lt.body) continue;
        let fx = random(-forceMagnitude, forceMagnitude);
        let fy = random(-0.0002 * intensity, 0.0002 * intensity);
        BodyM.applyForce(lt.body, lt.body.position, { x: fx, y: fy });
        BodyM.setVelocity(lt.body, {
          x: constrain(lt.body.velocity.x, -8 * intensity, 8 * intensity),
          y: constrain(lt.body.velocity.y, -12 * intensity, 12 * intensity)
        });
      }
    } else {
      for (let lt of letters) {
        if (!lt.body) continue;
        BodyM.setVelocity(lt.body, { x: constrain(lt.body.velocity.x, -30, 30), y: constrain(lt.body.velocity.y, -50, 50) });
      }
    }

    // 🕳️ Colapso natural + audio
    if (!finalCollapseTriggered && elapsed >= 38) {
      finalCollapseTriggered = true;

      // Detener audio principal y reproducir collapse.mp3
      if (timeAudio && typeof timeAudio.stop === 'function') try { timeAudio.stop(); } catch (e) {}
      if (heartAudio && typeof heartAudio.stop === 'function') try { heartAudio.stop(); } catch (e) {}
      if (collapseSound && collapseSound.isLoaded()) { collapseSound.play(); collapseStartTime = millis(); }

      // Quitar constraints de letras
      for (let lt of letters) {
        if (lt.constraint) { WorldM.remove(world, lt.constraint); lt.constraint = null; }
      }

      // Gravedad leve
      if (engine && engine.world && engine.gravity) engine.gravity.y = 1.2;

      // Pequeño impulso inicial
      for (let lt of letters) {
        if (lt.body) BodyM.applyForce(lt.body, lt.body.position, { x: random(-0.005, 0.005), y: random(-0.01, 0) });
      }

      console.log('💥 Colapso final activado: letras caen naturalmente');
    }

    if (elapsed >= TOTAL_TIME && !audioEnded) { audioEnded = true; console.log('TOTAL_TIME alcanzado — audioEnded = true'); }
  }

  // 🔤 Dibujar letras
  for (let lt of letters) {
    if (!lt.body) continue;
    manageLetterVisibilityAndReentry(lt);
    drawLetter(lt);
  }
}


/* ===================== HUD simplificado ===================== */
function drawHUD_simplified() {
  // Barra superior: fondo semi-transparente
  let barH = 46;
  push();
  noStroke();
  fill(0, 0, 0, 160);
  rect(0, 0, CANVAS_W, barH);

  // IZQUIERDA: título e instrucción (pequeño)
  fill(255);
  textSize(14);
  textAlign(LEFT, CENTER);
  text("Ansiedad", 12, barH / 2 - 6);
  textSize(12);
  fill(200);
  text("Presiona Espacio para iniciar", 12, barH / 2 + 12);

  // CENTRO: tiempo restante (grande)
  textAlign(CENTER, CENTER);
  if (started) {
    let elapsed = (millis() - startTime) / 1000;
    let secLeft = max(0, TOTAL_TIME - floor(elapsed));
    textSize(20);
    fill(255);
    //text(nf(secLeft, 2) + " s", CANVAS_W / 2, barH / 2 - 4);
    textSize(12);
    fill(200);
    //text("Tiempo restante", CANVAS_W / 2, barH / 2 + 12);
  } else {
    textSize(16);
    fill(230);
    text("Pausado", CANVAS_W / 2, barH / 2 - 2);
    textSize(12);
    fill(180);
    text("Presiona Espacio para comenzar", CANVAS_W / 2, barH / 2 + 12);
  }

  // DERECHA: fase actual (normal / paralisis)
    textAlign(RIGHT, CENTER);
  if (collapseHUDUpdated) {
    fill(100, 180, 255);
    textSize(14);
    text("Respira", CANVAS_W - 12, barH / 2 - 2);
    textSize(11);
    fill(200);
    text("Ya pasó...", CANVAS_W - 12, barH / 2 + 12);
  } else if (finalPhaseStarted) {
    fill(255, 180, 40);
    textSize(14);
    text("Pánico", CANVAS_W - 12, barH / 2 - 2);
    textSize(11);
    fill(200);
    text("¡No sé que hacer!", CANVAS_W - 12, barH / 2 + 12);
  } else if (started) {
    fill(120, 255, 140);
    textSize(14);
    text("Somatización", CANVAS_W - 12, barH / 2 - 2);
    textSize(11);
    fill(200);
    text("Estoy temblando...", CANVAS_W - 12, barH / 2 + 12);
  } else {
    fill(200);
    textSize(12);
    text("Listo", CANVAS_W - 12, barH / 2);
  }

  pop();

  // Barra de progreso inferior (única, clara)
  /*let pbX = 12, pbW = CANVAS_W - 24, pbY = CANVAS_H - 20, pbH = 10;
  fill(0, 0, 0, 150);
  noStroke();
  rect(pbX, pbY, pbW, pbH, 6);
  let progress = 0;
  if (started) {
    let elapsed = (millis() - startTime) / 1000;
    progress = constrain(elapsed / TOTAL_TIME, 0, 1);
  } else progress = 0;
  fill(255, 200);
  rect(pbX, pbY, pbW * progress, pbH, 6);

  // Texto pequeño sobre la barra de progreso (centrado)
  push();
  textSize(12);
  fill(20);
  textAlign(CENTER, CENTER);
  text((int(progress * 100)) + "%", CANVAS_W / 2, pbY + pbH / 2);
  pop();*/
}

/* ===================== start / restart ===================== */
function startOrRestart() {
  heartAudioStarted = false;
  if (!MATTER_LOADED) {
    console.warn('Matter no listo.');
    return;
  }
  try { canvasElement.elt.focus(); } catch(e) {}

  // Evitar duplicar audio: detener si ya suena
  if (timeAudio && typeof timeAudio.isPlaying === 'function' && timeAudio.isPlaying()) {
    try { timeAudio.stop(); } catch(e) {}
  }

  // Reproducir audio en su estado normal, rate=1
  if (timeAudio && typeof timeAudio.isLoaded === 'function' && timeAudio.isLoaded()) {
    try { timeAudio.setVolume(1); timeAudio.rate(1); timeAudio.loop(); } catch(e) { console.warn(e); }
  }

  // Eliminar bodies/constraints de letras previas, sin tocar mouseConstraint ni ground
  for (let lt of letters) {
    if (lt.constraint) { try { CompositeM.remove(world, lt.constraint); } catch(e) {} lt.constraint = null; }
    if (lt.body) { try { CompositeM.remove(world, lt.body); } catch(e) {} lt.body = null; }
    lt.hidden = true;
    lt.spawnTime = null;
  }

  spawnIndex = 0;
  // dejamos lastSpawnAt en millis() - SPAWN_INTERVAL para comportamiento normal,
  // pero también reseteamos la bandera que forzará el primer spawn a START_DELAY.
  lastSpawnAt = millis() - SPAWN_INTERVAL * 1000;
  firstSpawnTriggered = false;   // importante: permitir el primer spawn al segundo 2
  startTime = millis();
  started = true;
  finalPhaseStarted = false;
  console.log('Inicio/reinicio ejecutado.');
}

/* ===================== spawnLetter ===================== */
function spawnLetter(index) {
  let lt = letters[index];
  let sizeW = lt.size.w, sizeH = lt.size.h;
  let startX = lt.anchor.x + random(-20,20);
  let startY = lt.anchor.y - 180 + random(-30,30);

  let zone = lt.anchor.y < CANVAS_H * 0.4 ? 0 : (lt.anchor.y < CANVAS_H * 0.6 ? 1 : 2);
  let frictionByZone = zone === 0 ? 0.01 : (zone === 1 ? 0.05 : 0.16);
  lt.desiredFriction = frictionByZone;

  let body = BodiesM.rectangle(startX, startY, sizeW, sizeH, {
    restitution: LETTER_RESTITUTION,
    friction: frictionByZone,
    frictionAir: 0.01,
    mass: 1
  });

  lt.body = body;
  lt.hidden = false;
  lt.spawnTime = millis();

  let spring = ConstraintM.create({
    bodyA: body,
    pointB: { x: lt.anchor.x, y: lt.anchor.y },
    stiffness: SPRING_STIFFNESS,
    damping: SPRING_DAMPING,
    length: 0,
    render: { visible: false }
  });

  lt.constraint = spring;
  WorldM.add(world, [body, spring]);

  // Retroceso leve en otras letras
  for (let other of letters) {
    if (other === lt) continue;
    if (other.body) {
      let dx = other.body.position.x - body.position.x;
      let dy = other.body.position.y - body.position.y;
      let m = sqrt(dx*dx + dy*dy) + 0.1;
      let fx = (dx/m) * 0.0005 * random(0.6, 1.2);
      let fy = (dy/m) * 0.0002 * random(-0.8, 0.8);
      BodyM.applyForce(other.body, other.body.position, { x: fx, y: fy });
    }
  }
}

/* ===================== distracciones progresivas exponenciales ===================== */
function applyDistractionToAllLettersProgressive() {
  if (!started) return;

  // Tiempo transcurrido en segundos
  let elapsed = (millis() - startTime) / 1000;

  // Fracción de tiempo total (0 → 1)
  let tfrac = constrain(elapsed / TOTAL_TIME, 0, 1);

  // Crecimiento exponencial de la intensidad
  // Empieza muy suave y sube bruscamente hacia el final
  let intensity = map(pow(tfrac, 4), 0, 1, 0.1, 2.5);

  for (let lt of letters) {
    if (!lt.body) continue;

    // Fuerza lateral aleatoria con dirección variable
    let dir = random() > 0.5 ? 1 : -1;
    let fx = dir * LATERAL_FORCE_MAG * intensity * random(0.8, 1.2);

    BodyM.applyForce(lt.body, lt.body.position, { x: fx, y: 0 });

    // Impulsos verticales (saltos nerviosos)
    // Más frecuentes y más fuertes hacia el final
    let jumpChance = map(pow(tfrac, 3), 0, 1, 0.002, 0.07);
    if (random() < jumpChance) {
      BodyM.applyForce(lt.body, lt.body.position, { 
        x: 0, 
        y: -0.004 * intensity * random(0.8, 1.5) 
      });
    }

    // Pequeña rotación aleatoria adicional que también crece con el tiempo
    if (random() < 0.05 * intensity) {
      BodyM.setAngularVelocity(lt.body, random(-0.1, 0.1) * intensity);
    }
  }
}

/* ===================== ocultamiento / reentrada ===================== */
function manageLetterVisibilityAndReentry(lt) {
  let b = lt.body;
  if (!b) return;
  let margin = 30;
  if (!lt.hidden) {
    if (b.position.x < -margin || b.position.x > CANVAS_W + margin || b.position.y > CANVAS_H + margin) {
      lt.hidden = true;
      lt.exitSide = b.position.x < -margin ? 'left' : (b.position.x > CANVAS_W + margin ? 'right' : 'bottom');
      b.isSensor = true;
      lt.reentryAt = millis() + random(600, 1200);
    }
  } else {
    if (millis() >= lt.reentryAt) {
      if (lt.exitSide === 'left') {
        BodyM.setPosition(b, { x: -60, y: lt.anchor.y + random(-40, 40) });
        BodyM.setVelocity(b, { x: 3 + random(0,1), y: -0.5 });
      } else if (lt.exitSide === 'right') {
        BodyM.setPosition(b, { x: CANVAS_W + 60, y: lt.anchor.y + random(-40, 40) });
        BodyM.setVelocity(b, { x: -3 - random(0,1), y: -0.5 });
      } else {
        BodyM.setPosition(b, { x: lt.anchor.x + random(-40, 40), y: CANVAS_H + 60 });
        BodyM.setVelocity(b, { x: random(-1,1), y: -6 - random(0,2) });
      }
      setTimeout(() => { if (b) b.isSensor = false; }, 400);
      lt.hidden = false;
      let dx = lt.anchor.x - b.position.x;
      let dy = lt.anchor.y - b.position.y;
      let m = sqrt(dx*dx + dy*dy) + 0.1;
      BodyM.applyForce(b, b.position, { x: (dx/m) * 0.003, y: (dy/m) * 0.003 });
    }
  }
}

/* ===================== fase final ===================== */
function enterFinalPhase() {
  finalPhaseStarted = true;
  for (let lt of letters) {
    if (lt.constraint) {
      lt.constraint.stiffness = SPRING_STIFFNESS * 8;
      lt.constraint.damping = SPRING_DAMPING * 3;
    }
    if (lt.body) BodyM.setVelocity(lt.body, { x: lt.body.velocity.x * 0.2, y: lt.body.velocity.y * 0.2 });
  }
  if (timeAudio && typeof timeAudio.isLoaded === 'function' && timeAudio.isLoaded()) {
    try { timeAudio.rate(MAX_AUDIO_RATE); } catch(e) {}
  }
}

/* ===================== finalize word ===================== */
function finalizeWord() {
  for (let lt of letters) {
    if (lt.constraint) {
      lt.constraint.stiffness = SPRING_STIFFNESS * 12;
      lt.constraint.damping = SPRING_DAMPING * 4;
    }
    if (lt.body) {
      let dx = lt.anchor.x - lt.body.position.x;
      let dy = lt.anchor.y - lt.body.position.y;
      let m = sqrt(dx*dx + dy*dy) + 0.1;
      BodyM.applyForce(lt.body, lt.body.position, { x: (dx/m) * 0.02, y: (dy/m) * 0.02 });
    }
  }
}

/* ===================== dibujo letra ===================== */
function drawLetter(lt) {
  let b = lt.body;
  if (!b) return;
  if (lt.hidden && abs(b.position.x) > CANVAS_W + 50) return;
  push();
  translate(b.position.x, b.position.y);
  rotate(b.angle);
  rectMode(CENTER);
  fill(30,30,30,220);
  rect(0, 0, lt.size.w, lt.size.h, 6);
  fill(255);
  noStroke();
  textSize(textSizeBase);
  text(lt.char, 0, 0);
  pop();
}

/* ===================== p5 keyPressed fallback ===================== */
function keyPressed() {
  if (keyCode === 32) {
    startOrRestart();
    return false;
  }
}


/* ===================== Paredes ===================== */
function createCanvasWalls() {
  const thickness = 50; // grosor suficiente
  const options = { isStatic: true, restitution: 0.4, friction: 0.5 };

  // Pared superior
  const wallTop = BodiesM.rectangle(CANVAS_W / 2, -thickness / 2, CANVAS_W, thickness, options);
  // Pared inferior
  const wallBottom = BodiesM.rectangle(CANVAS_W / 2, CANVAS_H + thickness / 2, CANVAS_W, thickness, options);
  // Pared izquierda
  const wallLeft = BodiesM.rectangle(-thickness / 2, CANVAS_H / 2, thickness, CANVAS_H, options);
  // Pared derecha
  const wallRight = BodiesM.rectangle(CANVAS_W + thickness / 2, CANVAS_H / 2, thickness, CANVAS_H, options);

  WorldM.add(world, [wallTop, wallBottom, wallLeft, wallRight]);
}



/* ===================== fase de colapso natural ===================== */
function triggerFinalCollapse() {
  if (finalCollapseTriggered) return;
  finalCollapseTriggered = true;

  console.log("💥 Colapso final activado.");

  // Detener el audio si sigue sonando
  if (timeAudio && typeof timeAudio.stop === 'function') {
    try { timeAudio.stop(); } catch (e) { console.warn(e); }
  }

  // Quitar constraints (resortes) para dejar caer las letras libremente
  for (let lt of letters) {
    if (lt.constraint) {
      try { WorldM.remove(world, lt.constraint); } catch (e) {}
      lt.constraint = null;
    }
  }

  // Aumentar ligeramente la gravedad para una caída más natural
  if (engine && engine.world && engine.gravity) {
    engine.gravity.y = 1.2;
  }

  // Dar un pequeño impulso aleatorio a cada letra
  for (let lt of letters) {
    if (lt.body) {
      BodyM.applyForce(lt.body, lt.body.position, {
        x: random(-0.005, 0.005),
        y: random(-0.01, 0)
      });
    }
  }
}
```

## Captura de pantalla representativa

<img width="998" height="748" alt="image" src="https://github.com/user-attachments/assets/f64260c8-32be-47b5-b30e-f707d72a46f4" />

<img width="1000" height="751" alt="image" src="https://github.com/user-attachments/assets/8baaccd6-fb9a-4bfa-9fde-c6619bf2aae5" />

## GIF
[Aquí está mi obra en GIF](https://jumpshare.com/s/2TGVvn8MI2RagWVtDzgz)


## Autoevaluación:
__Mi nota es:__ __5,0__. Porque cumplí satisfactoriamente con todas las actividades de la Unidad.
Primero, analicé las obras de Ji Lee y usandolas de fuente de inspiración, surgieron y plantee dos posibles palabras con representaciones visuales interesantes. Luego, realicé los experimentos propuestos usando los referentes webs indicados y luego explicando una variedad de conceptos aplicados en estos. Finalmente, realicé el Apply tomando un camino de diseño muy conceptual desde lo que me imaginé en un principio con respecto a la ansiedad y como podía usarla para representar las sensaciones y sintomas físicos derivados de esta.




