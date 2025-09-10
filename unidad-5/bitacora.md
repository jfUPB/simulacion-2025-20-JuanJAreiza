# Evidencias de la unidad 5

## Actividad 02.

### Parte 1.
#### ¿Cómo se está gestionando la creación y la desaparción de las partículas y cómo se gestiona la memoria en cada una de las simulaciones?

1. En este primer caso, se crea primero un arreglo que contendra todas las particulas que se generen. Luego en el draw se llama a ese arreglo para crear una nueva partícula dentro de esta con una posición incial en el centro superior de la pantalla. Dentro de cada partícula hay un "lifespan" que se interpreta como una esperanza de vida. Dentro del mismo Draw se comprueba por medio de un for "inverso" -es decir, que hace su recorrido del index restando en vez de sumar, para evitar saltarse comprobaciones de cada partícula- si la partícula está muerta y en caso de que sí, es eliminada de la memoría. Para poder llegar a ese estado de "muerta" ocurre bajando en cada frame 2 unidades del valor del lifespan, el método de la partícula isDead devuelve conocer el lifespan si está como < 0.0. (REPASAR)
