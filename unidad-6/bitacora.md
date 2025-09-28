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
> Tu respuesta aquí:
> 

## Enlace a la obra en el editor de p5.js

[Aquí está mi obra]()

## Código de la obra 

``` js

```

## Captura de pantalla representativa








