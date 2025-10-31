# Evidencias de la unidad 8

## Actividades

* __Actividad 1.__

> * __Le Parody & Alba G. Corral | Dimension N__

> __1.__ Encuentro múltiples relaciones tanto particulares como comunes entre las dos obras. Por ejemplo, la aparición de ciertos elementos dentro del canvas sigue el ritmo de la música de manera precisa, ajustándose al BPM casi al pie de la letra.

> También se observa una conexión clara entre las frecuencias sonoras y la intensidad o volumen de la música: los sonidos agudos y graves provocan variaciones en los trazos que se generan en el canvas, modificando su ángulo o dirección. Sin embargo, estos trazos siempre se acompañan entre sí, como si fueran pinceladas que, aunque compuestas por formas irregulares y distintas, funcionan en armonía visual.

> En "Le Parody & Alba G. Corral", por ejemplo, noto la presencia de un círculo blanco que reacciona a ciertos tonos específicos o a alguna interacción de la intérprete. Este elemento no sigue un patrón rítmico constante, sino que parece responder a otro tipo de parámetro, aunque nunca pierde su presencia dentro de la composición general.

> También es interesante cómo el fondo estrellado, con apariencia de galaxia, reacciona al ritmo musical. Las partículas generadas parecen tener cierto grado de incertidumbre en su velocidad de desplazamiento, lo que hace que cada trazo responda de manera distinta. No obstante, todos conservan la sincronía con la música, y además parecen seguir patrones de simetría vertical, generando reacciones grupales que recuerdan a un tiling o mosaico visual.

> En cuanto al color, en varias ocasiones los cambios no parecen directamente ligados al ritmo o la música, sino que responden a una lógica más aleatoria. Sin embargo, esta aleatoriedad está contenida dentro de una estructura: si la paleta propuesta incluye cinco colores, cada uno aparece de forma aparentemente azarosa, pero respetando proporciones previamente establecidas dentro de la composición visual.

> __2.__ Considero que la mayoría de los elementos que se generan en el fondo para completar la composición pueden clasificarse como generativos. En contraste, he notado que casi todos los elementos principales —como las figuras o los trazos más prominentes— parecen estar interpretados en tiempo real.

> ¿Por qué pienso que los elementos de fondo son generativos? Porque los percibo más rítmicos que melódicos. Algunos de ellos funcionan como si representaran instrumentos de base, como la batería o el bajo: siguen un pulso constante y mantienen el BPM durante toda la pieza, aportando estructura sin depender de variaciones melódicas.

> En el caso específico de Dimension N, por ejemplo, observo que la amplitud de la onda que se va desarrollando a lo largo de la obra tiene un comportamiento generativo. En cambio, la interpretación parece centrarse más en la transformación y evolución de los visuales principales a medida que avanza la obra, lo que sugiere una interacción directa con ciertos momentos o pasajes musicales.

> __3.__ El hecho de que los visuales se generen en tiempo real junto con la música me transmite una sensación de naturalidad, relajación e inmersión dentro de la canción. Siento que ambas dimensiones, audio y visual, no solo coexisten, sino que se construyen mutuamente en el mismo instante, lo que genera una experiencia mucho más viva y poderosa a los sentidos.

> Además, al notar que ciertos elementos parecen ser interpretados y otros generativos, se crea un equilibrio interesante entre lo predefinido y lo espontáneo. Esto aporta una tensión creativa muy estimulante; lo que estoy viendo no podrá repetirse de la misma forma en otro momento.

> En conclusión, esta sincronía e interpretación en tiempo real potencia la expresividad de la obra y hace que la relación con el espectador sea más directa, emocional y única. Es un puro performance que no solo se escucha y se ve, sino que se siente.
> 

* __Actividad 2.__

> 1. La canción que usaré para dar vida a la composición será: __Blitzkrieg Bop__ de __The Ramones__. [Aquí está la canción en Youtube](https://www.youtube.com/watch?v=NQDPx_k66w4)

> 2. Quiero conseguir una visual que se sienta entre organica y con mucha influencia del estilo Brutalista del diseño gráfico. Líneas y que se sienta entre futurista grunge, pero con el suficiente movimiento para representar la intensidad y ritmo crudo de mi selección musical.

> 3. Quiero usar el mouse por ser una herramienta rápida y fácil de usar. Pienso primeramente en los clicks y la rueda del mouse. También algunas teclas que puedan accionar comportamientos variados y complementarios de la escena para seguir una parte mucho mas mélodica.

> 4. Tengo pensado usar __Partículas__ para complementar los espacios y generar cuerpos reactivos a la música. La obra va a partir de una __generación fractal__ como la vista en clase y vista en varias referencias buscadas por mi parte, para crear simetrias y figuras particulares por cada generación. Quiero usar una geometría polar, para que todo el movimiento se sienta comprimido en el centro con posibilidad de dispersarse por todo el Canvas. Para que esta estructura se sienta viva y reaccione a la música, pienso usar __Ruido Perlin__. La idea inicial es que la fuerza de la canción, cambie la amplitud de este. Tengo pensado en que se generen 5 estructuras de forma predeterminada, pensado mucho en el estilo Brutalism y de ahí se generen las distorsiones con la música y por el usuario. Para que los cambios de cada estructura sean suaves/interpolados, tengo pensado usar __Lerp__.

> 5. __Mis bocetos:__
> <img width="1396" height="1508" alt="12" src="https://github.com/user-attachments/assets/32a859cd-cc05-4734-ab1d-a2c92550e75f" />
> <img width="1396" height="980" alt="13" src="https://github.com/user-attachments/assets/31d7ab48-1161-4497-840c-48e54cdac7aa" />

> Los inputs van a afectar los colores, la densidad de trazos, la cantidad de figuras y sus propias formas para dar variedad constante a toda la escena. Especificamente (será llenado cuando sepa que usar):
> * __Click izquierdo__ para cambiar de interpretación geométrica.
> * __Click derecho__ para explosión de partículas momentáneas.
> * __Rueda del mouse__ para cambiar la __cantidad de "lados" o trazos__ de la figura.
> * __Q y A__ para __cambiar la paleta de colores__ a una de Brutalismo (blanco) y otra Grunge (colores psicodélicos)
> * __Flechas arriba y abajo__ para cambiar la __velocidad de cambio de color__ (en modo Grunge).

---


## Apply

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra](https://editor.p5js.org/JuanJAreiza/sketches/TAaxukMtV)

## Código de la obra 

``` js
let song;
let fft;
let amplitude;
let peakDetect;

// Audio Analysis variables
let lowEnergy = 0, midEnergy = 0, highEnergy = 0, rms = 0;
const BANDS = { low: [20, 200], mid: [200, 2000], high: [2000, 8000] };
const SENSITIVITY_ONSET = 0.5; 
const BPM_TARGET = 120; 
let beatCounter = 0;
let lastBeatTime = 0;

// Visual variables
let fractalGenerator; 
const BASE_RADIUS = 150; 
const POINTS_PER_BRANCH = 50; 
const FRACTAL_DEPTH = 3; 

// Simetría dinámica
let currentSymmetryCount = 8; 

// Modos de fractal
let currentFractalMode = 0;
const TOTAL_FRACTAL_MODES = 5; 

// Transición
let targetFractalMode = 0; 
let transitionProgress = 1.0; 
const TRANSITION_SPEED = 0.05; 

// Psychedelic specific variables
let FEEDBACK_ALPHA = 50; // Ahora variable let para ajuste con teclado
let COLOR_CYCLE_SPEED = 2; // Ahora variable let para ajuste con teclado
let currentHue = 0;

// Partículas (pooling)
let particles = []; 
const MAX_PARTICLES_TOTAL = 500; 
let particlePool = [];

let isFullscreenActive = false;
let isMonochrome = false;


class Particle {
    constructor() {
        this.active = false;
        this.pos = createVector();
        this.vel = createVector();
        this.life = 0;
        this.maxLife = 0;
        this.size = 0;
        this.hue = 0;
    }

    activate(x, y, vx, vy, life, size, hue) {
        this.active = true;
        this.pos.set(x, y);
        this.vel.set(vx, vy);
        this.life = life;
        this.maxLife = life;
        this.size = size;
        this.hue = hue;
    }

    update() {
        if (!this.active) return;
        this.pos.add(this.vel);
        this.vel.mult(0.98); 
        this.life--;
    }

    display() {
        if (!this.active) return;
        const alpha = map(this.life, 0, this.maxLife, 0, 255);
        noStroke();
        fill(this.hue, 255, 255, alpha); 
        square(this.pos.x, this.pos.y, this.size); 
    }
}

/**
 * Clase para generar el patrón fractal circular reactivo de líneas.
 */
class FractalGenerator {
    constructor(baseRadius, pointsPerBranch, fractalDepth) {
        this.baseRadius = baseRadius;
        this.pointsPerBranch = pointsPerBranch;
        this.fractalDepth = fractalDepth;
        this.time = 0;
        
        this.previousShapeR = [];
        this.currentShapeR = []; 
        this._initializeShapeArrays();
    }
    
    _initializeShapeArrays() {
        const totalPoints = this.pointsPerBranch + 1;
        for (let i = 0; i < totalPoints; i++) {
            this.previousShapeR[i] = this.baseRadius;
            this.currentShapeR[i] = this.baseRadius;
        }
    }

    update() {
        this.time += 0.01 + midEnergy * 0.05 + highEnergy * 0.02; 
        
        if (transitionProgress < 1.0) {
            transitionProgress += TRANSITION_SPEED;
            transitionProgress = min(transitionProgress, 1.0);
        }
    }

    display(mode, symmetryCount) {
        push();
        translate(width / 2, height / 2); 
        
        rotate(this.time * 0.5 + highEnergy * 0.5); 
        const globalScale = 1 + lowEnergy * 0.5; 
        scale(globalScale);

        for (let s = 0; s < symmetryCount; s++) {
            rotate(TWO_PI / symmetryCount); 
            
            this._drawFractalBranch(this.baseRadius, 1, currentFractalMode, targetFractalMode, symmetryCount);

            if (s % 2 === 0) { 
                scale(-1, 1);
            }
        }
        pop();
    }
    
    /**
     * Calcula la forma base de los radios para un modo dado.
     */
    _calculateShape(baseRadius, depth, mode) {
        const shapeRadii = [];
        const distortionAmount = lowEnergy * 50; 
        const distortionSpeed = midEnergy * 0.5;
        const lowFactor = 1.0 + lowEnergy * 1.5; 
        
        for (let i = 0; i <= this.pointsPerBranch; i++) {
            const angle = map(i, 0, this.pointsPerBranch, 0, TWO_PI);
            
            const noiseFactor = noise(cos(angle) * 0.5 + this.time * distortionSpeed, 
                                      sin(angle) * 0.5 + this.time * distortionSpeed, 
                                      depth * 0.1) * 2 - 1; 

            let r = baseRadius + noiseFactor * distortionAmount; 

            // Aplicar lógica de 5 Formas Brutalistas
            if (mode === 0) { // Muro Vibrante (Circular)
                r += sin(angle * (2 + lowEnergy * 5) + this.time * 2) * (10 + highEnergy * 20) * lowFactor;
            } else if (mode === 1) { // Estructura Angular (Cristal)
                const segments = currentSymmetryCount;
                const phase = angle / (TWO_PI / segments);
                r = baseRadius * 1.2 + cos(phase * TWO_PI) * (10 + lowEnergy * 50) + noiseFactor * 20;
            } else if (mode === 2) { // Espiral Pesada (Túnel)
                const spiralEffect = sin(angle * 3 + this.time * 5) * (80 + midEnergy * 100);
                r = baseRadius * 0.8 + spiralEffect * lowFactor; 
            } else if (mode === 3) { // Bloque Asimétrico (Pulsos)
                r += cos(angle * 2 + this.time * 4) * (20 + highEnergy * 40);
                r += sin(angle * 5 + this.time * 2) * (10 + lowEnergy * 30);
                r = lerp(r, baseRadius, 0.2 + lowEnergy * 0.5); 
            } else if (mode === 4) { // Ladrillo Cíclico (Cuadrados)
                const brickEffect = sin(angle * 10 + this.time * 8) * (20 + midEnergy * 50);
                r = baseRadius + brickEffect * lowFactor;
            }
            shapeRadii.push(r);
        }
        return shapeRadii;
    }

    /**
     * Dibuja una "rama" del fractal, con recursión simulada y LÍNEAS INTERPOLADAS.
     */
    _drawFractalBranch(currentRadius, depth, currentMode, targetMode, symmetryCount) {
        if (depth > this.fractalDepth) return; 

        // 1. Calcular la forma actual y la forma objetivo
        const currentRadii = this._calculateShape(currentRadius, depth, currentMode);
        const targetRadii = this._calculateShape(currentRadius, depth, targetMode);

        // --- Estilo de Línea (Brutalismo de Líneas) ---
        noFill(); 
        let strokeHue;
        let strokeSaturation;
        let strokeBrightness;

        if (isMonochrome) {
            // Modo Monocromático: Blanco puro
            strokeHue = 0;
            strokeSaturation = 0; // Sin color
            strokeBrightness = 255; // Blanco
        } else {
            // Modo Color: Usa el ciclo normal
            strokeHue = (currentHue + depth * 30) % 360;
            strokeSaturation = 255; 
            strokeBrightness = 255;
        }

        stroke(strokeHue, strokeSaturation, strokeBrightness, 255);
        strokeWeight(map(rms, 0, 1, 1, 4) * (1 / depth) + 1); 

        beginShape();
        for (let i = 0; i <= this.pointsPerBranch; i++) {
            const angle = map(i, 0, this.pointsPerBranch, 0, TWO_PI);
            
            const r_interp = lerp(targetRadii[i], currentRadii[i], transitionProgress);
            
            const x = cos(angle) * r_interp;
            const y = sin(angle) * r_interp;
            
            vertex(x, y);
        }
        endShape(CLOSE);

        // Llamadas recursivas
        const numSubBranches = 2 + floor(lowEnergy * 2); 
        for (let j = 0; j < numSubBranches; j++) {
            push();
            rotate(TWO_PI / numSubBranches + this.time * 0.1 * midEnergy); 
            scale(0.5 + lowEnergy * 0.1); 
            this._drawFractalBranch(currentRadius * 0.5, depth + 1, currentMode, targetMode, symmetryCount); 
            pop();
        }
    }
    
    /**
     * Función llamada al hacer click para preparar la transición.
     */
    startTransition(newMode) {
        currentFractalMode = targetFractalMode;
        targetFractalMode = newMode;
        transitionProgress = 0.0;
    }
}


// --------------------------------------------------------------------
// FUNCIONES P5.JS (Nuevas Interacciones)
// --------------------------------------------------------------------

function preload() {
    song = loadSound('song.mp3');
}

function setup() {
    createCanvas(windowWidth, windowHeight);
    colorMode(HSB, 360, 255, 255, 255); 
    
    frameRate(45); 

    // --- Audio Setup ---
    fft = new p5.FFT(0.8, 1024);
    amplitude = new p5.Amplitude();
    peakDetect = new p5.PeakDetect(0.005, SENSITIVITY_ONSET, 60); 

    // --- Visual Setup ---
    fractalGenerator = new FractalGenerator(BASE_RADIUS, POINTS_PER_BRANCH, FRACTAL_DEPTH); 
    currentSymmetryCount = 8; 
    
    // CAMBIO CLAVE: Llama a loop() aquí para que el dibujo inicie inmediatamente.
    loop(); 
}

function mousePressed() {
    // La lógica de inicio de la simulación y música se movió a keyTyped().
    // mousePressed() ahora solo maneja la interactividad:

    // A. CLIC IZQUIERDO (LEFT) - Cambia la forma y simetría.
    if (mouseButton === LEFT) {
        let nextMode = (targetFractalMode + 1) % TOTAL_FRACTAL_MODES;
        
        // Mantiene la lógica de simetría basada en el modo
        if (nextMode === 0) currentSymmetryCount = 4;
        else if (nextMode === 1) currentSymmetryCount = 8;
        else if (nextMode === 2) currentSymmetryCount = 3;
        else if (nextMode === 3) currentSymmetryCount = 6;
        else if (nextMode === 4) currentSymmetryCount = 12;

        // Inicia la transición (Cambio de forma)
        fractalGenerator.startTransition(nextMode);
        background(255, 255, 255, 50); 
    } 
    
    // B. CLIC DERECHO (RIGHT) - Ejecuta el efecto de partículas.
    else if (mouseButton === RIGHT) {
        triggerInteractionEffect(mouseX, mouseY);
    }
}

// --- NUEVA FUNCIÓN PARA ACTIVAR MÚSICA Y PANTALLA COMPLETA ---
function keyTyped() {
    // A. ACTIVACIÓN DE PANTALLA COMPLETA con 'P'
    if (key === 'p' || key === 'P') {
        if (!isFullscreenActive) {
            fullscreen(true);
            
            // Asegura que el lienzo se reajuste al tamaño de la pantalla completa
            windowResized(); 
            
            isFullscreenActive = true;
            console.log("Pantalla completa activada con tecla P.");
        }
    } 
    
    // B. ACTIVACIÓN DE MÚSICA con 'ESPACIO'
    else if (key === ' ' && song.isLoaded() && !song.isPlaying()) {
        // La música comienza independientemente de si la pantalla completa está activa.
        song.play();
        console.log("Música activada con tecla ESPACIO.");
    }
}

/**
 * Nueva función para control de teclado. (Interacción 1)
 */
function keyPressed() {
    // Control de velocidad de ciclo de color
    if (keyCode === UP_ARROW) {
        COLOR_CYCLE_SPEED = 10; // Velocidad Máxima
        console.log("Color Speed: 10 (MÁX)");
    } else if (keyCode === DOWN_ARROW) {
        COLOR_CYCLE_SPEED = 0; // Color Fijo / Sin Ciclo
        console.log("Color Speed: 0 (FIJO)");
    }
    
    // Control de densidad de estela (Feedback Alpha)
    else if (key === 'q' || key === 'Q') {
        isMonochrome = true;
        console.log("Modo: MONOCROMÁTICO (Brutalismo Puro)");
    } else if (key === 'a' || key === 'A') {
        isMonochrome = false;
        console.log("Modo: COLOR CÍCLICO (Psicodélico)");
    } else if (key === 's' || key === 'S') {
        saveCanvas('obraFinal', 'jpg');
        console.log("Guardado pantallazo");
    }
}

/**
 * Nueva función para control de rueda del ratón. (Interacción 5)
 */
function mouseWheel(event) {
    if (event.delta < 0) {
        // Scroll Up (Aumenta simetría)
        currentSymmetryCount = min(currentSymmetryCount + 1, 12);
    } else {
        // Scroll Down (Disminuye simetría)
        currentSymmetryCount = max(currentSymmetryCount - 1, 3); // Mínimo 3 lados
    }
    console.log("Symmetry Count:", currentSymmetryCount);
    // Previene que la página se desplace
    return false; 
}


function draw() {
    // --- 0. Feedback ---
    background(0, 0, 0, FEEDBACK_ALPHA); 

    // --- 1. Control de Color y Tiempo ---
    const currentSketchTime = millis(); 
    const timeSinceLastBeat = currentSketchTime - lastBeatTime;
    const beatInterval = 60000 / BPM_TARGET; 

    // El color cycling ahora usa la variable modificable
    currentHue = (currentHue + COLOR_CYCLE_SPEED + midEnergy * 5) % 360; 

    if (timeSinceLastBeat >= beatInterval) {
        lastBeatTime = currentSketchTime - (timeSinceLastBeat % beatInterval);
        beatCounter++;
    }

    // --- 2. Análisis de Audio ---
    fft.analyze();
    rms = amplitude.getLevel();
    lowEnergy = fft.getEnergy(BANDS.low[0], BANDS.low[1]) / 255;
    midEnergy = fft.getEnergy(BANDS.mid[0], BANDS.mid[1]) / 255;
    highEnergy = fft.getEnergy(BANDS.high[0], BANDS.high[1]) / 255;

    // Detección de Onset
    peakDetect.update(fft);
    if (peakDetect.isDetected) {
        background(255, 255, 255, 200); 
        triggerInteractionEffect(width / 2, height / 2); 
    }

    // --- 3. Actualización y Renderizado del Fractal ---
    fractalGenerator.update();
    // La simetría es controlada por el modo o por mouseWheel
    fractalGenerator.display(currentFractalMode, currentSymmetryCount); 

    // --- 4. Dibujar Partículas ---
    for (let i = particles.length - 1; i >= 0; i--) {
        particles[i].update();
        particles[i].display();
        
        if (!particles[i].active) {
            particlePool.push(particles[i]);
            particles.splice(i, 1);
        }
    }
}

// --------------------------------------------------------------------
// FUNCIONES AUXILIARES (POOLING)
// --------------------------------------------------------------------

function getParticleFromPool(x, y, vx, vy, life, size, hue) {
    let p;

    if (particlePool.length > 0) {
        p = particlePool.pop();
    } 
    else if (particles.length < MAX_PARTICLES_TOTAL) {
        p = new Particle();
    }
    else {
        p = particles.shift();
    }

    if (p) {
        p.activate(x, y, vx, vy, life, size, hue);
        
        if (particles.indexOf(p) === -1) {
            particles.push(p);
        }
    }
}

function triggerExplosion(x, y, count) {
    for (let i = 0; i < count; i++) {
        const angle = random(TWO_PI);
        const speed = random(5, 15);
        getParticleFromPool(
            x + random(-10, 10), y + random(-10, 10),
            cos(angle) * speed,
            sin(angle) * speed,
            random(30, 90), 
            random(3, 5), 
            currentHue + random(-30, 30) % 360
        );
    }
}

function triggerInteractionEffect(x, y) {
    background(255, 255, 255, 100); 
    triggerExplosion(x, y, 30);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

document.addEventListener('contextmenu', event => event.preventDefault());
```

## Captura de pantalla representativa
![obraFinal (2)](https://github.com/user-attachments/assets/f09d305b-f06a-477b-b39a-44b189760bd8)

![obraFinal (5)](https://github.com/user-attachments/assets/3e825c86-40c2-4db3-a91d-11e90e8d7c92)

![obraFinal](https://github.com/user-attachments/assets/e5478615-96cb-4857-991b-659486b7262e)



## Autoevaluación:
__Mi nota es:__ __5,0__. Porque cumplí satisfactoriamente con las tres actividades. Primero, analicé dos videos que llamaron mi atención, extraje varias ideas y conceptos que me parecieron muy interesantes para transmitir sensaciones y me sirvieron como fuente de inspiración para desarrollar la última actividad (Apply). Además, realicé la segunda actividad de manera que me permitiera generar buenas ideas y bases sólidas para crear un visualizer de una canción que me gusta mucho, lo cual me acercó bastante al resultado que tenía en mente desde el inicio.


