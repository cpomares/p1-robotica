# Práctica 4: Descomposición modular

**Duración**: 2 semanas

### Ejercicio 1 ###

Implementa un programa que pida 3 números enteros que representarán los extremos de 2 intervalos. El primer intervalo estará formado por el menor de los 3 números y el de valor intermedio, y el segundo intervalo por el de valor intermedio y el de mayor valor. Ten en cuenta que los números introducidos pueden estar desordenados.

Después se imprimirá por pantalla para cada intervalo, todos los números múltiplos de un número introducido por teclado que haya dentro de cada intervalo.

Paso a paso, el programa tiene que hacer lo siguiente:

- Leer los datos de los intervalos
- Leer el múltiplo del primer intervalo
- Leer el mútiplo del segundo intervalo
- Imprimir los múltiplos del primer intervalo
- Imprimir los múltiplos del segundo intervalo


**Ejemplo de ejecución:**

~~~text
Introduce 3 números enteros (separados por un espacio en blanco): 30 20 10
¿Qué múltiplo quieres utilizar para el intervalo [10, 20]: 2
¿Qué múltiplo quieres utilizar para el intervalo [20, 30]: 3
Los múltiplos de 2 en el intervalo [10, 20] son:
10 12 14 16 18 20 
Los múltiplos de 3 en el intervalo [20, 30] son:
21 24 27 30
~~~

**Casos de prueba:**

~~~text
Entrada:
30 20 10
2
3

Salida por pantalla:
10 12 14 16 18 20 
21 24 27 30
~~~

~~~text
Entrada:
25 50 8
0
5
4

Salida por pantalla:
10 15 20 25
28 32 36 40 44 48
~~~

~~~text
Entrada:
17 9 35
12
7

Salida por pantalla:
12
21 28 35
~~~

### Ejercicio 2 ###

Vamos a implementar el juego de Nim (simplificado). El Nim es un juego clásico de estrategia que se supone originario de Oriente. Sus reglas, en nuestra versión modificada, son las siguientes: 

1. Se tienen tres montones de palillos, cada uno de los cuales contiene, al principio del juego, entre 3 y 6 palillos. El número inicial de palillos en cada montón lo determinará el ordenador al azar y puede variar de una partida a otra, pero siempre habrá un mínimo de 3 y un máximo de 6. 
2. El jugador humano elige un montón y quita 1 ó 2 palillos. 
3. Después, el ordenador hace lo mismo: elige un montón y quita 1 ó 2 palillos. 
4. Los pasos 2 y 3 se repiten hasta que sólo queda un palillo o ninguno en total. El jugador que deba retirar el último palillo o no quede ninguno, pierde.

**Ejemplo de ejecución:**

~~~text
El turno es del Humano
El contenido actual de los montones es:
  Montón 1: 6 palillos
  Montón 2: 3 palillos
  Montón 3: 6 palillos
¿De qué montón quieres quitar palillos (1, 2 ó 3)? 2
¿Cuántos palillos quieres quitar (1 ó 2)? 2
El turno es de la Máquina
El contenido actual de los montones es:
  Montón 1: 6 palillos
  Montón 2: 1 palillos
  Montón 3: 6 palillos
Es mi turno.
Elijo quitar 1 palillos del montón 2
El turno es del Humano
El contenido actual de los montones es:
  Montón 1: 6 palillos
  Montón 2: 0 palillos
  Montón 3: 6 palillos
¿De qué montón quieres quitar palillos (1, 2 ó 3)? 1
¿Cuántos palillos quieres quitar (1 ó 2)? 1
El turno es de la Máquina
El contenido actual de los montones es:
  Montón 1: 5 palillos
  Montón 2: 0 palillos
  Montón 3: 6 palillos
Es mi turno.
Elijo quitar 1 palillos del montón 3
El turno es del Humano
El contenido actual de los montones es:
  Montón 1: 5 palillos
  Montón 2: 0 palillos
  Montón 3: 5 palillos
¿De qué montón quieres quitar palillos (1, 2 ó 3)? 1
¿Cuántos palillos quieres quitar (1 ó 2)? 2
El turno es de la Máquina
El contenido actual de los montones es:
  Montón 1: 3 palillos
  Montón 2: 0 palillos
  Montón 3: 5 palillos
Es mi turno.
Elijo quitar 1 palillos del montón 3
El turno es del Humano
El contenido actual de los montones es:
  Montón 1: 3 palillos
  Montón 2: 0 palillos
  Montón 3: 4 palillos
¿De qué montón quieres quitar palillos (1, 2 ó 3)? 1
¿Cuántos palillos quieres quitar (1 ó 2)? 2
El turno es de la Máquina
El contenido actual de los montones es:
  Montón 1: 1 palillos
  Montón 2: 0 palillos
  Montón 3: 4 palillos
Es mi turno.
Elijo quitar 1 palillos del montón 3
El turno es del Humano
El contenido actual de los montones es:
  Montón 1: 1 palillos
  Montón 2: 0 palillos
  Montón 3: 3 palillos
¿De qué montón quieres quitar palillos (1, 2 ó 3)? 3
¿Cuántos palillos quieres quitar (1 ó 2)? 2
El turno es de la Máquina
El contenido actual de los montones es:
  Montón 1: 1 palillos
  Montón 2: 0 palillos
  Montón 3: 1 palillos
Es mi turno.
Elijo quitar 1 palillos del montón 1
Enhorabuena!!!! Me has ganado
~~~

Las funciones que **como mínimo** debes crear son:

- `crearMontones`: se encarga de crear los 3 montones, asignándole a cada uno de ellos una cantidad aleatoria de palillos (entre 3 y 6). Devuelve los montones al main en los parámetros montón1, montón2 y montón3.
- `mostrarMontones`: muestra el contenido actual de los montones.
- `elegirMonton`: dependiendo del parámetro "turno", se encargará de pedir al usuario que elija un montón, o bien de lograr que el ordenador elija un motón al azar. Después, comprueba si el montón elegido es correcto. Si es así, devuelve el montón elegido al `main`. Si no, mostrará un mensaje de error ("Error: ese montón ya no tiene palillos") y volverá a pedir que se elija un montón.
- `elegirPalillos`: dependiendo del valor de "turno", le pide al usuario que elija el número de palillos que quiere retirar, o bien hace que el ordenador lo elija al azar. Ese número debe ser 1 ó 2. Tiene que comprobar que el número de palillos elegido es correcto. Si es así, se devuelve el número de palillos elegidos al `main`. Si no, se muestra un mensaje de error ("Error: ese montón no tiene tantos palillos") y se vuelve a pedir que se introduzca un número de palillos. 
- `quitarPalillos`: quita un número determinado de palillos de un montón.
- `comprobarFinJuego`: mira si, entre todos los montones, sólo queda por retirar un palillo. Si es así, el juego debe acabar y el ganador es el jugador que posee el turno actualmente. 
- El `main` os lo damos hecho. Se encarga de invocar a todos los demás en el orden adecuado. Además, irá restando de cada montón los palillos que se hayan retirado, y controlará cuándo debe finalizar el juego.

 
En el fichero que os hemos dejado en Moodle, tenéis el main completo que no debéis modificar y los prototipos de las funciones que como mínimo debéis implementar, así como las definiciones de los tipos de datos que vais a necesitar.

Comprueba el funcionamiento por separado de cada función antes de integrarlas en tu programa. **Puedes escribir todas las funciones adicionales que consideres conveniente**.

Para generar valores aleatorios, en C se utilizan las funciones `rand()` y `srand()`. Para ello:

- Se añaden las librerías `<stdlib.h>` y `<time.h>`.
- Antes de generar cualquier número aleatorio se añade la siguiente sentencia que inicializa la semilla para generar números aleatorios dependiendo del instante de tiempo en el que estamos ejecutando el programa.

~~~c
   srand(time(0));
~~~

- Para generar un valor aleatorio dentro del intervalo [a,b], puedes usar la función que os damos hecha:

~~~c
int numeroAleatorio(int a, int b) {
    return rand() % (b-a+1) + a;
}
~~~


----

Programación 1, Grado de Robótica, curso 2020-21  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
