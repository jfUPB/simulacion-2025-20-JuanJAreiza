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
> 

## Apply
> Tu respuesta aquí:
> La interacción se da principalmente con __el mouse__, que ejerce una __fuerza de atracción sobre el origen de los péndulos__. Según la posición del mouse en el Canvas, el origen se desplaza, generando variaciones adicionales en los trazos. Esa influencia no es igual en los dos ejes: en el eje X la fuerza está amplificada (*100), mientras que en el eje Y es más moderada (*50).

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra]()

## Código de la obra 

``` js

```

## Captura de pantalla representativa







