# Evidencias de la unidad 6

## Actividades

* __Actividad 1.__ De las obras de Tyler Hobbs, ¿cuáles te llamen la atención y por qué? ¿Qué te inspira de su trabajo?:
> <img width="900" height="598" alt="Captura de pantalla 2025-09-24 091052" src="https://github.com/user-attachments/assets/243ac39c-75a5-4382-85f1-ab3265d1a928" />
> <img width="747" height="559" alt="Captura de pantalla 2025-09-24 091410" src="https://github.com/user-attachments/assets/746a1436-daac-480b-a0df-9f63749ab5a2" />

> Estas dos obras fueron las más atractivas para mi, principalmente por el estilo tan remarcado que tiene cada una.
> Por un lado, tenemos unos trazos muy órganicos, como simulando el producto de un pincel con pintura. Por algún motivo me da vibras con sus patrones, colores y la textura, de una pintura asiatica de los 80's. Sus patrones son 

> Del mismo modo, la segunda obra me atrae principalmente por la técnica usando puntos. Los patrones que se crean me parecen muy interesantes con cada evolución de los colores y respetando el espacio de cada elemento, siendo consciente de corregir la posibilidad de que se sobreescriban.


>- 

> 

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
> Busco inspirarme en una combinación de elementos acúaticos, como son:

> Toda la inspiración nace desde un vídeo que ví en TikTok, donde se podían ver una gran cantidad de peces y colores muy bellos:
> https://github.com/user-attachments/assets/f80d63b2-a5ff-4c49-9e6e-7a61960fa1fa

> Otro punto de motivación fueron los juguetes que se veían mucho cuando estaba pequeño, que consistían en una caja de agua en donde se debía de encajar aros de colores en diferentes puntos por medio de impulsos de agua. Normalmente con fondos muy coloridos y llamativos. Estos juguetes en inglés tienen el nombre de Aqua Rings Toys, no sé muy bien como llamarlo en español Jajaj:

> <img width="800" height="800" alt="image" src="https://github.com/user-attachments/assets/e1e3626d-184d-4d2b-985f-4d13ebc875d2" />

> También tuve inspiración de diferentes escenas de películas de mi infancia como Nemo o La Sirenita.

> A partir de eso, quería hacer una escena con mucho movimiento, pero que mi participación fuera puramente en visuales y que el fondo tuviera independencia en su vida y movimiento.

> MOTHER - DANZIG, SHOULD I STAY OR SHOULD I GO

Necesito que me crees un prompt basado en esta idea de creación para p5.js que escribí. Pregúntame todas las dudas que puedas quedar en el aire para que sea un prompt muy completo y claro:
> HACERLO CON NODOS, TIENE QUE SONAR TODA LA CANCIÓN (La canción es Should I Stay or Should I Go). DIVIDIRLO EN 3 O 4 MOMENTOS: Primero, solo hay boids en un flow field que se mueven y el angulo de los vectores de flow field se mueven con la música, se puede influir en el movimiento (PENSAR MEJOR) (EL VOLUMÉN INFLUYE LA VELOCIDAD DE LOS BOIDS). Luego, con flocking (en el momento donde rompe la canción) poner un depredador que persigue a todos los boids. Sus logaritmos de alineación, cohesión y separación van a ser influidos por la posición del mouse. Para el tercer momento, que entren desde arriba "redes" o "figuras" que capturan a los peces y los sacan del Canvas, provocando que al final, no quede ninguno en escena, nisiquiera el depredador.

CHATGPT ME DICE:
🎵 GENERALIDADES SOBRE LA MÚSICA

¿Tienes un archivo de audio específico de “Should I Stay or Should I Go”?

¿Lo vas a cargar localmente o desde una URL?

¿Hay problemas legales con el uso de esa canción? (Alternativamente, ¿quieres que sea una canción genérica con características similares?)

¿Cuáles son los momentos de la canción que definen el cambio de escena?

¿Tienes los timestamps de cuándo ocurren esos 3 o 4 momentos?

¿Se usan cambios de volumen, ritmo, frecuencia o algo más para detectarlos?

¿Se debe reproducir toda la canción sí o sí, o puede cortarse al terminar la animación?

🌀 MOMENTO 1: BOIDS EN FLOW FIELD

¿Qué tipo de flow field quieres?

¿Perlin noise en 2D?

¿Vector field generado por FFT (análisis de audio en frecuencia)?

¿Qué tan denso debe ser el campo? (ej. 20x20, 40x40 celdas)

Los boids:

¿Tienen apariencia específica (colores, formas, partículas, etc.)?

¿Tienen colas o efectos visuales (trails, glow, etc.)?

"El volumen influye en la velocidad de los boids":

¿Quieres que el volumen controle directamente la velocidad lineal?

¿O que afecte la aceleración máxima o algún otro parámetro?

¿Qué significa "se puede influir en el movimiento (PENSAR MEJOR)"?

¿Quieres que el usuario pueda controlar algo más (con el mouse, teclas, etc.)?

🦈 MOMENTO 2: DEPREDADOR Y FLOCKING

¿El depredador tiene forma especial?

¿Debe ser más grande, de otro color, con animación?

¿Qué sucede si el depredador alcanza a un boid?

¿Lo elimina? ¿Lo "absorbe"? ¿Solo lo persigue?

"Logaritmos de alineación, cohesión y separación" influenciados por el mouse:

¿Quieres que la posición del mouse controle directamente los pesos de esas fuerzas?

Por ejemplo: eje X = alineación, eje Y = cohesión, clic = separación

¿O que el mouse atraiga/repela a los boids?

¿El depredador también es un boid con flocking o es una entidad totalmente distinta?

🕸 MOMENTO 3: REDES O FIGURAS QUE ATRAPAN

¿Qué forma tienen estas "redes"?

¿Son figuras geométricas, formas orgánicas, animaciones?

¿Caen desde arriba con gravedad o de forma controlada?

¿Cómo “capturan” a los boids?

¿Colisión directa?

¿A través de un área de atracción?

¿Animación tipo trampa?

¿Qué pasa con los boids capturados?

¿Desaparecen?

¿Se los lleva la red fuera del canvas?

¿Cuántas redes deben aparecer? ¿Una gran red al final o múltiples redes pequeñas?

¿También debe desaparecer el depredador?

¿Es capturado o desaparece de otra forma?

🌟 FINAL

¿Hay un efecto final?

¿El canvas queda vacío?

¿Una transición visual, cambio de color, fade out?

¿Debe reiniciarse la animación o termina definitivamente?

⚙️ OTROS DETALLES TÉCNICOS

¿Tamaño del canvas? ¿Es responsive?

¿Modo de visualización? ¿Pantalla completa? ¿Integrado en una web?

¿Quieres usar la librería de p5.js pura o alguna extensión (como p5.sound, p5.gui, etc.)?

¿Te interesa que esto sea interactivo para otros usuarios, como en una web pública?




YO RESPONDO:
1. Se va a cargar localmente. Y no, no hay problemas legales.
2. Sí. La canción completa dura: 3 min 9 seg (3:09). Primer momento iría de: 0 a 1:07. Segundo momento iría de: 1:08 a 2:21. Tercer momento iría de: 2:22 a 3:09.
3. Tiene que sonar toda la canción sí o sí.
4. El flowfield que manejan en Nature of Code, que esté influenciado por el FFT. Y el campo debe tener una densidad de 25x25.
5. Sí, los boids son pequeños ovalos con trails. Cada uno con cada color y los trails con glow.
6. Sí, quiero que el volúmen afecte la velocidad lineal directamente.
7. 


## Enlace a la obra en el editor de p5.js

[Aquí está mi obra]()

## Código de la obra 

``` js
LÓGICA PARA CAMBIAR DE MOMENTO:
let momento = 0;  // Variable que controla el estado o momento
let tiempoCambio = 0;

function setup() {
  createCanvas(400, 400);
  tiempoCambio = millis();  // Guardamos el tiempo inicial
}

function draw() {
  background(220);
  
  // Cambiar de momento automáticamente cada 5 segundos
  if (millis() - tiempoCambio > 5000) {
    momento++;
    if (momento > 2) momento = 0;  // Reinicia el ciclo de momentos
    tiempoCambio = millis();       // Reinicia el contador de tiempo
  }

  // Lógica por momento
  switch (momento) {
    case 0:
      momentoUno();
      break;
    case 1:
      momentoDos();
      break;
    case 2:
      momentoTres();
      break;
  }
}

function momentoUno() {
  fill(255, 0, 0);
  ellipse(width/2, height/2, 100);
  text("Momento 1: Círculo rojo", 10, 20);
}

function momentoDos() {
  fill(0, 255, 0);
  rect(100, 100, 200, 200);
  text("Momento 2: Cuadro verde", 10, 20);
}

function momentoTres() {
  fill(0, 0, 255);
  triangle(200, 100, 300, 300, 100, 300);
  text("Momento 3: Triángulo azul", 10, 20);
}


LÓGICA PARA HACERLO MANUAL:
function keyPressed() {
  if (key === ' ') {  // Espacio para avanzar de momento
    momento++;
    if (momento > 2) momento = 0;
  }
}

```

## Captura de pantalla representativa











