# Práctica 7: Punteros y memoria dinámica

**Duración**: 2 semanas

## Memoria dinámica en funciones

Cuando pasamos un array o puntero como parámetro a una función, estamos pasando la dirección de memoria del primer elemento del array, pero no al puntero en sí, que es una copia. Es decir, no podríamos modificar dinámicamente su memoria porque no tenemos una referencia a la misma.

Es decir, si sólo queremos trabajar con los elementos, lo haríamos como hemos hecho hasta ahora. Pero si dentro de una función queremos modificar la memoria dinámicamente (usando `malloc`, `realloc`, etc) necesitamos pasar el array o puntero por referencia.

Ejemplo:

~~~c
#define TAM 20

void creaVector(int **);

int main() {
   int *vector;

   // Reservamos la memoria
   creaVector(&vector);
   vector[0] = 1;  //Rellenamos al azar
   vector[2] = 2;
   printf("Pos 2: %d\n", vector[2]); //Comprobamos

   // Liberamos memoria
   free(vector);
   vector = NULL;

   return 0;
}

void creaVector(int **v) {
   *v = (int*)malloc(sizeof(int) * TAM);
}
~~~

Podéis ampliar esta explicación en el apartado [Punteros y funciones]((https://cpomares.github.io/p1-robotica/Teoria/tema07-punteros-y-memoria-dinamica/tema07-punteros-y-memoria-dinamica.html#3-punteros-y-funciones)) del tema 7 de los apuntes.

## Ejercicio 1

A partir de la solución que os proporcionamos del ejercicio 5 de la práctica 5, modifica el programa para que permita realizar la suma de números binarios de cualquier número de dígitos, en lugar de estar restringidos a una longitud máxima de 8 bits.

Intenta realizar los mínimos cambios posibles. Para ello, usa esta nueva definición del tipo `TPalabra`:

~~~c
typedef char* TPalabra;
~~~

y utiliza las mismas funciones ya implementadas, modificando si es necesario los prototipos de algunas de ellas y su definición. Puedes añadir alguna otra función si lo consideras conveniente.


Ejemplos de ejecución:

~~~text
Introduce palabra de bits: 1000101010101010101010101010100000001
Introduce palabra de bits: 10101000000101010101010


     1000101010101010101010101010100000001
   + 0000000000000010101000000101010101010
     -------------------------------------
     1000101010101101010010101111110101011

Introduce palabra de bits: 1101000111110001010111
Introduce palabra de bits: 1100010000000010000110


     1101000111110001010111
   + 1100010000000010000110
     ----------------------
    11001010111110011011101


Introduce palabra de bits: f
Fin del programa
~~~

## Ejercicio 2

A partir del programa implementado en el ejercicio anterior, modifícalo para que utilice esta nueva definición del tipo `TPalabra`:

~~~c
typedef struct {
    char *bits;
    int  lon;
} TPalabra;
~~~

## Ejercicio 3

Modifica el ejercicio 3 de la práctica 5 utilizando memoria dinámica, de forma que las filas del calendario sólo se creen cuando se necesiten y no quede ninguna vacía. Utiliza las siguientes definiciones:

~~~c
#define COL 7

typedef int TFilaCalendario[COL];
typedef TFilaCalendario *TCalendario;
~~~

Ahora el tipo `TCalendario` es un array dinámico de tipo `TFilaCalendario` (que a su vez es un array estático de 7 elementos).

Si partes de la solución que os proporcionamos, sólo debes modificar dos funciones además del `main()`. Es posible que debas modificar el prototipo de alguna más, puedes hacerlo, pero modificando mínimamente su código.

Ejemplos de ejecución:

~~~text
Introduce mes: 10
Introduce año: 2020

 LUN MAR MIE JUE VIE SAB DOM

   .   .   .   1   2   3   4
   5   6   7   8   9  10  11
  12  13  14  15  16  17  18
  19  20  21  22  23  24  25
  26  27  28  29  30  31   .
~~~

~~~text
Introduce mes: 11
Introduce año: 2020

 LUN MAR MIE JUE VIE SAB DOM

   .   .   .   .   .   .   1
   2   3   4   5   6   7   8
   9  10  11  12  13  14  15
  16  17  18  19  20  21  22
  23  24  25  26  27  28  29
  30   .   .   .   .   .   .
~~~

----

Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
