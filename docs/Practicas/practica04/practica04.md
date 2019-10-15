# Práctica 4: Descomposición modular

**Duración**: 2 semanas

### Ejercicio 1 ###

Implementa un programa, modularizado en funciones, que pida 2 intervalos de números `[a,b]` comprobando que son válidos, es decir, que `a < b`, e imprima los valores de ambos intervalos de forma intercalada. Ten en cuenta que el tamaño de los intervalos puede ser distinto.

**Ejemplo de ejecución:**

~~~text
Introduce valores del intervalo 1: 0 5
Introduce valores del intervalo 2: 10 12
0 10 1 11 2 12 3 4 5
~~~

Datos de entrada: `2 intervalos válidos`

**Casos de prueba:**

~~~text
Entrada:
7 2
3 8
20 30

Salida por pantalla:
3 20 4 21 5 22 6 23 7 24 8 25 26 27 28 29 30
~~~

~~~text
Entrada:
100 108
6 2
2 6

Salida por pantalla:
100 2 101 3 102 4 103 5 104 6 105 106 107 108
~~~

~~~text
Entrada:
11 15
1 5

Salida por pantalla:
11 1 12 2 13 3 14 4 15 5
~~~

### Ejercicio 2 ###

1. Escribe una función que lea un mes (1-12) y un año (1900-2100) por teclado y los devuelva.
2. Modifica el ejercicio 2 de la práctica 2 para convertirlo en una función que reciba un mes como parámetro y devuelva el número de días que tiene. Añade la comprobación para los años bisiestos:  son bisiestos todos los años múltiplos de 4, excepto aquellos que son múltiplos de 100 pero no de 400.
3. Utilizando las funciones anteriores, escribe un programa completo que lea un mes y un año y muestre por pantalla el calendario correspondiente a ese mes. Para ello, vamos a utilizar el algoritmo de Zeller que, dada una fecha (dia-mes-año) te devuelve el día de la semana (1-lun, 7-dom). El algoritmo de Zeller te lo damos hecho en la siguiente función:

~~~c
int zeller (int dia, int mes, int anyo) {
  int a, m, y, primerDia;

  a = (14-mes) / 12;
  y = anyo - a;
  m = mes + (12*a) - 2;
  primerDia = (dia + y + (y/4) - (y/100) + (y/400) + (31*m) / 12) % 7;

  if (primerDia == 0)  // domingo
    primerDia = 7;

   return primerDia;
}
~~~


**Ejemplo de ejecución:**

~~~text
Introduce mes: 10
Introduce año: 2019

 LUN MAR MIE JUE VIE SAB DOM
   .   1   2   3   4   5   6
   7   8   9  10  11  12  13
  14  15  16  17  18  19  20
  21  22  23  24  25  26  27
  28  29  30  31
~~~

Datos de entrada: `mes`, `año`

**Casos de prueba:**

~~~text
Introduce mes: 22
Introduce mes: 18
Introduce mes: 3
Introduce año: 2020

 LUN MAR MIE JUE VIE SAB DOM
   .   .   .   .   .   .   1
   2   3   4   5   6   7   8
   9  10  11  12  13  14  15
  16  17  18  19  20  21  22
  23  24  25  26  27  28  29
  30
~~~

~~~text
Introduce mes: 2
Introduce año: 2020

 LUN MAR MIE JUE VIE SAB DOM
   .   .   .   .   .   1   2
   3   4   5   6   7   8   9
  10  11  12  13  14  15  16
  17  18  19  20  21  22  23
  24  25  26  27  28  29
~~~

~~~text
Introduce mes: 2
Introduce año: 2019

 LUN MAR MIE JUE VIE SAB DOM
   .   .   .   .   1   2   3
   4   5   6   7   8   9  10
  11  12  13  14  15  16  17
  18  19  20  21  22  23  24
  25  26  27  28
~~~

### Ejercicio 3 ###

Implementa un programa que irá pidiendo 4 caracteres para representar un número binario de 4 bits. En caso de haberse introducido 4 dígitos binarios, se dibujarán en pantalla con un determinado alto y ancho que habrá sido solicitado previamente. Si algún carácter introducido no es un dígito binario, el programa terminará.

**Pista**: Partiendo de la solución del ejercicio 4 de la práctica anterior, modulariza dicho programa.
Tres de las funciones que incluyas (deberías definir más de 3), deberían realizar lo siguiente:

- una función para imprimir una determinada fila para el número 1
- otra función para imprimir la separación entre los números en cualquier fila
- otra función para imprimir una determinada fila para el número 0.


**Ejemplo de ejecución:**

~~~text
Introduce alto [15..30] y ancho [8..20] de los números: 15 8
Introduce número binario de 4 bits: 1 0 1 0

...#.....########........#.....########
..##.....#......#.......##.....#......#
.#.#.....#......#......#.#.....#......#
#..#.....#......#.....#..#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....#......#........#.....#......#
...#.....########........#.....########

Introduce número binario de 4 bits: 0 0 1 1

########.....########........#........#
#......#.....#......#.......##.......##
#......#.....#......#......#.#......#.#
#......#.....#......#.....#..#.....#..#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
#......#.....#......#........#........#
########.....########........#........#

Introduce número binario de 4 bits: 2 1 1 1
Fin del programa
~~~

----

Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
