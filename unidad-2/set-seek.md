# Unidad 2

## 🔎 Fase: Set + Seek


Cambiamos la aceleración cada frame para que cambie la dirección del elemento, por la suma de las fuerzas de aceleración.

### Actividad 1 REVISAR BIEN:
- Se actualizan los componentes de position con esta línea: "position.add(velocity);", donde se le agrega la referencia del vector que quiero sumar, toma su información.

Si la posición el eje x es mayor que el ancho de la pantalla o a la izquierda, la velocidad se invierte para que se direccione al lado contrario.(if (position.x > width || position.x < 0) {
    velocity.x = velocity.x * -1;
  }
  if (position.y > height || position.y < 0) {
    velocity.y = velocity.y * -1;
  }
  
- Porque la suma(+) no sabe interpretar la suma de vectores en este lenguaje.

Que cambie la dirección con el mouse.

### Actividad 2:
- Se reemplazó las propiedades de posición del objeto en "x" y "y", por una variable que crea un vector y se le da la misma información x y y, así queda contenida dentro de la variable directamente. Luego en la aleatoriedad del Walk, se agrega la variable en la suma de cada paso en Eje X y eje y.
  
-El código a continuación:

´´´
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

### Actividad 3:
- Primeramente se imprime en consola el valor de posición actual que fue anteriormente creado y corresponde a los valores de 6,9.
- Luego deberia imprimir 20, 30, debido a que se le envía la referencia de posición a una función llamada PlayingVector que cambia los valores de x y y de position.

- Se cumplió la hipotesis.

- Paso por valor es aquel en donde solo se comparte directamente un dato.
- Paso por referencia es aquel que se le da a una función para que manipule.

### Actividad 4:
- El método mag() sirve para calcular la magnitud del vector. La diferencia entre mag() y magSq() radica en que este da el mismo resultado, pero al cuadrado. La más eficiente puede ser cualquira, dependiendo del fin con el que se quiera usar.

- Cambia la escala del vector.

- La función dot calcula el producto punto entre dos vectores, es decir, entrega un número que dice cuanto coinciden o no dos vectores.

- Es una operación entre dos vectores que genera otro vector perpendicular a estos y su magnitud es igual al área del paralelogramo formado por los dos vectores originales.

- dist() sirve para calcular la distancia entre dos puntos.

- Limita la magnitud de un vector a una valor máximo.

Sitios de interés:
Threejs.org
cables.gl
