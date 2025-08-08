# Unidad 2

## 🔎 Fase: Set + Seek

Cambiamos la aceleración cada frame para que cambie la dirección del elemento, por la suma de las fuerzas de aceleración.

### Actividad 1:
- Los componentes del vector position se actualizan con la línea position.add(velocity); lo que significa que a la posición actual se le suma la referencia de la velocidad.

``` js
// Si la posición el eje x es mayor que el ancho de la pantalla o a la izquierda, la velocidad se invierte para que se direccione al lado contrario.

(if (position.x > width || position.x < 0) {
    velocity.x = velocity.x * -1;
  }
  if (position.y > height || position.y < 0) {
    velocity.y = velocity.y * -1;
  }
```
  
- Porque la suma (+) no sabe interpretar la suma de vectores en este lenguaje.

### Actividad 2:

- Se reemplazaron las propiedades individuales de posición en x y y por una sola variable que almacena un vector, utilizando createVector(x, y). De esta forma, la información de ambas coordenadas queda contenida directamente en un solo objeto. Luego, en el comportamiento aleatorio del "Walk", se actualiza la posición sumando directamente los valores aleatorios a los componentes del vector en los ejes X y Y.
  
-El código a continuación:

``` js
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.position = createVector(width/2, height/2);
    
    /*
    this.x = width / 2;
    this.y = height / 2;*/
  }

  show() {
    stroke(0);
    point(this.position);
  }

  step() {
    const choice = random(1);
    if (choice < 0.5) {
      this.position.x++;
    } else if (choice < 0.7) {
      this.position.x--;
    } else if (choice < 0.85) {
      this.position.y++;
    } else {
      this.position.y--;
    }
  }
}
```

### Actividad 3:
- Primero se imprime en consola el valor de la posición actual, que fue creada previamente con los valores 6, 9. Luego, debería imprimirse 20, 30, ya que la variable position se pasa como referencia a una función llamada PlayingVector, la cual modifica directamente los valores de x y y del vector.

- Se cumplió la hipótesis.

- El paso por valor ocurre cuando se envía una copia del dato a una función, por lo que cualquier cambio dentro de la función no afecta el valor original. El paso por referencia ocurre cuando se pasa a la función una referencia del dato original, lo que permite modificarlo directamente desde dentro de la función.

- Se está realizando un paso por referencia.

- Aprendí sobre la diferencia entre paso por valor, donde solo se pasa una copia de un dato, y paso por referencia, donde se comparte el acceso directo al objeto original.

### Actividad 4:
- El método mag() sirve para calcular la magnitud del vector. La diferencia entre mag() y magSq() radica en que este da el mismo resultado, pero al cuadrado. La más eficiente puede ser cualquira, dependiendo del fin con el que se quiera usar.

- Cambia la escala del vector.

- La función dot() calcula el producto punto entre dos vectores, es decir, entrega un número que dice cuanto coinciden o no dos vectores.

- Operación cruz es una operación entre dos vectores que genera otro vector perpendicular a estos y su magnitud es igual al área del paralelogramo formado por los dos vectores originales.

- dist() sirve para calcular la distancia entre dos puntos.

- limit() Limita la magnitud de un vector a una valor máximo.

### Actividad 5:

- Código a continuación:

``` js
let fI = 0;
let dirFI = 1;
let c1, c2;

function setup() {
    createCanvas(500, 500);
  
  c1 = color('red');
  c2 = color('blue');
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);
    let v1 = createVector(300, 0);
    let v2 = createVector(0, 300);
    let v3 = p5.Vector.lerp(v1, v2, fI);
  
    let vPerpendicular = p5.Vector.sub(v2, v1);
    let origenPerpendicular = p5.Vector.add(v0, v1);
  
    drawArrow(v0, v1, c1);
    drawArrow(v0, v2, c2);
    drawArrow(v0, v3, lerpColor(c1, c2, fI));
    drawArrow(origenPerpendicular, vPerpendicular, color('green'));
  
  fI += 0.01*dirFI;
  if(fI > 1) dirFI = -1;
  if(fI < 0) dirFI = 1;
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```

- lerp() usa 3 valores: dos de referencia y uno de ubicación entre los dos puntos de referencia. Al dibujarlo una vez, se cambia constantemente este último valor de forma gradual, generando una interpolación, es decir, un movimiento constante entre ambos puntos.

- lerpColor() funciona de modo similar: también usa tres valores (dos colores de referencia y un valor de "ubicación" entre ambos colores) para generar una transición gradual de color.

- drawArrow() considera la magnitud del vector. La flecha se ubica en la punta del vector, restando la distancia correspondiente al tamaño de la flecha que se le asigna. Luego, con ese punto como origen, se generan tres vectores en ese espacio que forman un triángulo, para que se interprete visualmente como una flecha.

### Actividad 6:
- El marco Motion 101 es un esquema básico para mover objetos mediante vectores. Solo dos pasos: 1. Añadir velocidad a la posición con position.add(velocity) y 2. Dibujar la nueva posición del objeto. Geométricamente la velocidad es un vector que le indica al objeto nueva dirección y rapidez en su movimiento, entonces a partir de la posición actual, se desplaza el objeto con su vector actualizado.
  
- En el objeto mover hay un vector de position que dice dónde está el objeto. Y un vector de velocidad que dice habia dónde se mueve y que tan rápido. Todo esto es llamado dentro del draw(), en mover.update(), que actualiza la posición sumando la velocidad.

### Actividad 7:
Se observa que la constante hace que cada vez la aceleración aumente mas hacia la derecha.
La aleatoria varía repentinamente y se desplaza como si tuviera vida, la noto muy órganica.
Con la que usa la posición del mouse, pareciera que tuviese gravedad hacia el cursor, como si estuviera orbitando al rededor de él.

#### Sitios de interés:
- Threejs.org
- cables.gl

