# Práctica 1: Tipos de datos simples

### Ejercicio 1 ###

El siguiente programa debe solicitar por teclado la edad, la inicial del nombre y la altura de una persona, y mostrará por pantalla su inicial y la suma de la edad y la altura. Completa la implementación de este programa rellenando cada hueco con la sentencia adecuada.

Después de completarlo, compílalo y ejecútalo para comprobar su correcto funcionamiento.

~~~c
#include <stdio.h>

int main() {
   ______________;
   ______________;
   ______________;


   printf("Introduce tu edad: ");
   ________________________;

   printf("Introduce la inicial de tu nombre: ");
   ________________________;

   printf("Introduce tu altura en metros: ");
   ________________________;


   printf("\n\nLa inicial de tu nombre es: %c\n",inicial);
   printf("La suma de tu edad y altura es: %.2f\n", edad + altura);

   return 0;
}
~~~

### Ejercicio 2 ###

Implementa un programa que solicite al usuario 3 caracteres y los muestre por pantalla en orden inverso al que han sido introducidos.

Ejemplo de ejecución:

~~~
Introduce 3 caracteres:
a b c
Los caracteres introducidos en orden inverso son:
c b a
~~~

Datos de entrada: `3 caracteres`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| a b c            | c b a              |
| 5 6 7            | 7 6 5              |   
| * > ?            | ? > *              |    


### Ejercicio 3 ###

Implementa un programa que solicite al usuario un número de años y muestre por pantalla las horas, minutos y segundos que tienen esa cantidad de años.

Ejemplo de ejecución:

~~~
Introduce número de años: 1
En 1 años hay 8760 horas, 525600 minutos y 31536000 segundos
~~~

Dato de entrada: `número de años`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
|1                 | En 1 años hay 8760 horas, 525600 minutos y 31536000 segundos              |
| 20               | En 20 años hay 175200 horas, 10512000 minutos, 630720000 segundos    |
| 100              | En 100 años hay 876000 horas, 52560000 minutos, 3153600000 segundos   |

### Ejercicio 4 ###

Implementa un programa que solicite al usuario las notas de los 3 exámenes de la convocatoria de Enero y muestre por pantalla la nota final de la asignatura en dicha convocatoria, teniendo en cuenta que las ponderaciones de los 3 exámenes son del 15%, 35% y 50% respectivamente.

Ejemplo de ejecución:

~~~
Introduce la nota del primer examen (temas 1 al 3): 4.3
Introduce la nota del segundo examen (temas 1 al 6): 5.5
Introduce la nota del tercer examen (temas 1 al 9): 5.0
La nota final en la convocatoria ordinaria de Enero es: 5.07
~~~

Datos de entrada: `nota1` `nota2` `nota3`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
|  4.3  5.5  5.0   | La nota final en la convocatoria ordinaria de Enero es: 5.07 |
|  7.0  4.0  3.5   | La nota final en la convocatoria ordinaria de Enero es: 4.20 |   
|  7.3  8.6  9.8   | La nota final en la convocatoria ordinaria de Enero es: 9.00 |  

### Ejercicio 5 ###

Escribe un programa que incluya un enumerado llamado TipoFigura con los tipos de figura circulo, cuadrado y triangulo.

Después imprime por pantalla el número asignado por el enumerado a cada figura.
Tienes que cambiar el número por defecto.

Ejemplo de ejecución:

~~~
Circulo: 1
Triangulo: 2
Cuadrado: 3
~~~

### Ejercicio 6 ###

Escribe un programa que pida por teclado los vértices de un triángulo y calcule e imprima por pantalla su perímetro (con dos decimales). Cada vértice consta de una coordenada x,y.

Para leer por teclado dos datos seguidos separados por una coma, puedes utilizar el scanf de la siguiente forma:

~~~c
scanf(“%d,%d”, &x, &y);
~~~

Para calcular el perímetro, primero debes obtener los tres lados mediante el cálculo de la distancia euclídea entre los tres vértices. La fórmula de la distancia euclídea es:

~~~c
distancia = sqrt((x2 - x1)*(x2 - x1) + (y2 - y1) * (y2 - y1));
~~~

`sqrt` es la función que calcula la raíz cuadrada. Para utilizarla, debes incluir la librería `<math.h>` a tu programa.

Ejemplo de ejecución:

~~~
Introduce el punto 1: 2,3
Introduce el punto 2: 4,5
Introduce el punto 3: 6,7
El perímetro del triángulo cuyos lados son (2,3)-(4,5)-(6,7) es 11.31
~~~

Datos de entrada: `x1,y1` `x2,y2` `x3,y3`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| 2,3 4,5 6,7      | El perímetro del triángulo cuyos lados son (2,3)-(4,5)-(6,7) es 11.31    |
| 2,2 4,4 8,8      | El perímetro del triángulo cuyos lados son (2,2)--(4,4)--(8,8) es 16.97  |   
| 8,4 3,5 7,6      | El perímetro del triángulo cuyos lados son (8,4)--(3,5)--(7,6) es 11.45  |


----

Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
