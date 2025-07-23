# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 1:
La aleatoriedad, en medio de un entorno de reglas y restricciones, brinda al sistema (y posteriormente al artista) la libertad y creatividad propias del arte. Permite que cada obra sea única, una nueva expresión que refleja, representa y da rienda suelta a la experimentación.

### Actividad 2:
- A pesar de las reglas perceptibles (como la intensidad de la música que influye en el brillo de las visuales), la aleatoriedad se manifiesta en la dirección y amplitud de cada una de las raíces. Aunque su crecimiento responde a normas definidas, estas se despliegan "libremente" sobre el lienzo. Incluso en la interacción del usuario hay un componente aleatorio, ya que los colores que se modifican varían de forma impredecible, haciendo que cada reproducción genere un resultado único y distinto.

- En el mundo del diseño UI/UX, aunque está regido por normas y lógicas bien establecidas, el diseño generativo puede funcionar como una herramienta poderosa para proponer múltiples soluciones a un mismo problema. También sería posible integrarlo directamente en los propios diseños, por ejemplo, por medio de pantallas o paneles con un alto grado de generación automática: interfaces únicas que se adaptan a cada usuario según sus necesidades, condiciones o intereses.

### Actividad 3:
- ¿Qué espero que suceda?
Modifiqué el codigo con el objetivo de que se agreguen mas agentes dentro del canva, que tengan una forma circular y que puedan varias su radio a partir del movimiento del eje X del mouse.

- ¿Qué sucedió?
Efectivamente aparecieron en escena 3 agentes nuevos, circulares y si se modifica su radio por el eje X del mouse.

- ¿Ocurrió lo que esperaba?
Si, pero al mismo tiempo me llevé una sorpresa porque el efecto visual que se crea al modificar el radio es cuanto menos, curioso. Ese no lo había previsto de ninguna manera.

### Actividad 4:
- La diferencia está principalmente en el comportamiento visual y estadístico. En la distribución uniforme, los datos suelen comportarse de forma similar, con poca variación y una probabilidad pareja para todos los valores. En cambio, en la no uniforme, la aleatoriedad genera un comportamiento más disperso, donde las probabilidades cambian y no siguen un patrón fijo. Visualmente, las gráficas se verían diferentes: una más rectangular y pareja, y la otra con picos más marcados e irregulares.

- Lo modifiqué usando probabilidades, donde la de dar un step hacia la derecha es del 50% y los demás porcentajes se distribuyen en las otras 3 direcciones. Usé un valor random entre 0-1 y quité el floor para evitar redondeos.

### Actividad 5:

Código:
let totalBoxs = 50;
let boxs = new Array(totalBoxs).fill(0);

function setup() {
  createCanvas(800, 400);
  background(255);
}

function draw() {
  let x = randomGaussian(320, 60);
  
  let i = floor(map(x, 0, width, 0, totalBoxs));
  if (i >= 0 && i < totalBoxs) {
    boxs[i]++;
  }
  
  background(255);
  let w = width / totalBoxs;
  for (let j = 0; j < totalBoxs; j++) {
    let h = boxs[j] * 3;
    rect(j * w, height - h, w - 1, h);
  }
}

Enlace: http://editor.p5js.org/JuanJAreiza/sketches/7t18PX7T8

Captura de pantalla:
<img width="1097" height="500" alt="image" src="https://github.com/user-attachments/assets/743ee148-4541-43c7-b10b-517bddbba560" />

### Actividad 6:

- ¿Por qué usar esta técnica? ¿Qué espero que suceda?
Usé está técnica en el primer ejercicio del Walker que era el que representaba mayor movimiento en el canva, con el objetivo de ver desplazamientos amplios en todo el espacio y disperso para cada agente creado.
Lo que espero que suceda es que con el cambio de color para cada Walker, se pueda diferenciar y crear pinceladas creativas en el lienzo, gracias a que puedan haber desplazamientos largos y cortos de forma aleatoria todo el tiempo. Además, ver de alguna manera el corrido que hace al haberle modificado la transparencia del propio color.

Código:
let walker;
let walker2;
let walker3;

function setup() {
  createCanvas(640, 240);
  walker = new Walker(color(255, 0, 0, 50));
  walker2 = new Walker(color(0, 255, 0, 50));
  walker3 = new Walker(color(0, 0, 255, 50));
  background(255);
}

function draw() {
  walker.step();
  walker.show();
  
  walker2.step();
  walker2.show();
  
  walker3.step();
  walker3.show();
}

class Walker {
  constructor(c) {
    this.x = width / 2;
    this.y = height / 2;
    this.c = c;
  }
  
  //Se podría hacer que haya impacto entre cada draw

  show() {
    noStroke();
    fill(this.c);
    circle(this.x, this.y, mouseX / 30);
  }

  step() {
    let stepSize;

    // 3% de probabilidad de un salto largo
    if (random(1) < 0.03) {
      stepSize = random(50, 150);
    } else {
      stepSize = random(1, 5);
    }

    let angle = random(TWO_PI);
    let dx = cos(angle) * stepSize;
    let dy = sin(angle) * stepSize;

    this.x += dx;
    this.y += dy;

    //Se limita para que no salga del Canva
    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }
}

Enlace: https://editor.p5js.org/JuanJAreiza/sketches/8GPFVNSlr

Captura de pantalla: <img width="1258" height="1030" alt="image" src="https://github.com/user-attachments/assets/3cf63b58-8138-47e0-9f97-3695905b38c7" />

### Actividad 7:

- Espero obtener el concepto mismo, es decir, una generación aleatoria de subidas y bajadas pero de una forma suavizada, que se desplace para que todo el tiempo se renueve y genere nuevo movimiento.

Código:
let xoff = 0;

function setup() {
  createCanvas(800, 400);
  stroke(0);
  noFill();
}

function draw() {
  background(255);
  beginShape();
  let offset = xoff;
  for (let x = 0; x < width; x++) {
    let y = noise(offset) * height; //Perlin, aleatorio pero suave. La altura para que considere todo el lienzo
    vertex(x, y); //Dibuja
    offset += 0.01;
  }
  endShape();

  xoff += 0.01; //Para que se mueva horizontal
}

Enlace: https://editor.p5js.org/JuanJAreiza/sketches/28DAGX24H

Captura de pantalla: <img width="1255" height="676" alt="image" src="https://github.com/user-attachments/assets/d0cf6a39-11e1-4be5-b3ef-317372659667" />
