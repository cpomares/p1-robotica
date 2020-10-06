
# Tema 3: Sentencias de control


## 1. Sentencias de control

 El **flujo de ejecución de un programa** define el orden que siguen las sentencias durante la ejecución del mismo.
 
En un determinado instante, el **estado de un programa** queda definido por el valor que tienen sus variables en ese momento. El estado de un programa es dinámico, y puede cambiar con la ejecución de sentencias dentro del mismo. Es **imprescindible realizar las sentencias adecuadas en el orden adecuado**.

La **estructura secuencial** es aquella en la que las instrucciones o sentencias se ejecutan una a una en el orden establecido.

Ejemplo:

~~~c
int valorA = 11, valorB = 4, resultado;resultado = valorA / valorB;valorA = valorA + 1; // resultado = 2
~~~No es lo mismo que:

~~~c
int valorA = 11, valorB = 4, resultado;valorA = valorA + 1;resultado = valorA / valorB; // resultado = 3
~~~


Se puede alterar esa secuencialidad usando estructuras no secuenciales, que permiten variar el flujo de control del programa dependiendo de ciertas condiciones. Las estructuras no secuenciales son:

- **Estructuras de selección**: Permiten que se tomen rutas alternativas de acción dependiendo del resultado de una
condición.
- **Estructuras de iteración**: Permiten repetir un conjunto de sentencias.

<img src="imagenes/estructuras_control.png" width="600px"/>


## 2. Estructuras de selección

Permiten que el programa determine las sentencias a ejecutar en base a determinadas **condiciones**.

Las condiciones se presentan como operadores relacionales (condiciones booleanas), integrando como operandos valores, variables o constantes.

Suponen una **bifurcación** en la secuencia de ejecución de las instrucciones de un programa

> Ejemplos donde se utilizan estructuras de selección:
>
> - Si el robot no tiene batería: ir a la zona de carga
> - Si el robot está cerca de un obstáculo: reducir su velocidad
> - Si el semáforo esta en rojo: detenernos, en cualquier otro caso: continuar

### Sentencia `if`

La sentencia `if` permite decidir qué secuencia de código se va a ejecutar a continuación en base a una condición.

La **sintaxis** de la sentencia `if` es:

~~~c
// Cuando la ejecución condicional afecta a una única línea

if (condicion_a_cumplir)
   instrucción a realizar;
~~~

~~~c
// Cuando la ejecución condicional afecta a una o más líneas

if (condicion_a_cumplir) {
   instrucción(es) a realizar;
}
~~~

La **semántica** (funcionamiento) del `if` es el siguiente:

- Si la `condicion_a_cumplir` devuelve un valor verdadero (o distinto de 0), se ejecutará la secuencia de instrucciones a realizar.
- Si la `condicion_a_cumplir`devuelve un valor falso (o 0), el `if`finalizará sin ejecutar la sencuencia de instrucciones asociada, pasándose a ejecutar la sentencia siguiente al `if`.

Como hemos comentado, el lenguaje C nativo no incorpora el tipo `bool`, por lo que tenemos que incluir la librería `#include <stdbool.h>`para trabajar con booleanos. La condición del `if` admite variables de otro tipo (`int`, `char`, `double`, ...) y se manejan como una variable `bool`, tomando el valor `false` si vale 0 o `true` para cualquier otro valor. No es aconsejable.

Ejemplo de sentencia `if`:

~~~c
bool fumador = true;double dineroAhorrado = 500;...if (fumador)   dineroAhorrado = 0;...if (dineroAhorrado > 1000 ) {   fumador = false;}
~~~

El uso de llaves es opcional si la instrucción a ejecutar tiene una única sentencia y es obligatorio si la instrucción tiene dos o más sentencias. Si no se añaden llaves, solamente la primera instrucción después del `if (condicion_a_cumplir)` será condicional: la segunda y sucesivas se ejecutarán siempre.

~~~c
bool condicionCumplida = false;

if (condicionCumplida)
   printf("Primera instrucción \n");
printf("Segunda instrucción \n"); // se ejecuta siempre
printf("Tercera instrucción \n"); // se ejecuta siempre

if (condicionCumplida) {
   printf("Primera instrucción \n");
   printf("Segunda instrucción \n");
   printf("Tercera instrucción \n");
}
~~~

La `condicion_a_cumplir` puede obtenerse mediante la combinación (usando operadores lógicos) de diferentes (sub)condiciones.Precedencia de operadores:

~~~text
1. ()2. *, /, %3. +, -4. <, <=, >, >= – ==, !=5. &&6. ||
~~~
Ejemplo:

~~~c++
bool oscuridad = true,
bateriaAgotada = false,
prioridad = false,
camaraEncendida = true;
int tiempoEnEspera = 100;
...
if(oscuridad || bateriaAgotada || (tiempoEnEspera>60 && !prioridad))   cameraEncendida = false;
~~~

Un programa con sentencias `if` puede visualizarse como un diagrama de la siguiente forma:

~~~c
instruccion_a;

if(condicion)   instruccionSiSeCumpleCondicion;

instruccion_b;instruccion_c;
~~~

<img src="imagenes/if.png" width="600px"/>

### Sentencia `if-else`


La sentencia `if-else`es una forma ampliada de la sentencia `if`. La utilizamos cuando tenemos instrucciones que sólo queremos que seejecuten cuando no se cumple la condición (opción `else`)

La **sintaxis** de la sentencia `if-else`es:

~~~c
if (condicion_a_cumplir) {
   instruccion(es)_a_ejecutar_condicion_verdadera;
}
else {
   instruccion(es)_a_ejecutar_condicion_falsa;
}
~~~

La **semántica** de la sentencia `if-else`es:

- Si la `condicion_a_cumplir`devuelve verdadero, se ejecuta `instruccion(es)_a_ejecutar_condicion_verdadera`.
- Si la `condicion_a_cumplir`devuelve falso, se ejecuta `instruccion(es)_a_ejecutar_condicion_falsa`.

El uso de llaves es idéntico a la sentencia `if`: opcional si la instrucción a ejecutar tiene una única sentencia y obligatorio si la instrucción tiene dos o más sentencias, tanto en la parte del `if`como en el `else`.

Ejemplo de `if-else`:

~~~c
int dineroAhorrado = 25500;int precioCoche = 15000;

if (dineroAhorrado < precioCoche)
   printf("Necesitas ahorrar, sólo tienes %d euros \n", dineroAhorrado);
else
   printf("Ya puedes comprarte el coche de %d euros \n", precioCoche);
~~~

Diagrama de sentencias `if-else`:

~~~c
instruccion_a;

if(condicion)
   instruccionSiSeCumpleCondicion;
else
   instruccionSiNoSeCumpleCondicion;

instruccion_b;
instruccion_c;
~~~

<img src="imagenes/if-else.png" width="600px"/>

### Sentencias `if` anidadas

También podemos anidar condiciones usando la combinación `else if`:

~~~c
double distancia;
...if(distancia<500)
   printf("Cerca \n");
else if(distancia<1500)
   printf("Distancia media \n");
else  printf("Lejos\n");
~~~

Diagrama sentencia `if anidada`:

<img src="imagenes/if-anidado.png" width="600px"/>

También podemos anidar `if-else` con esta estructura, dependiendo del problema:

~~~c
if ( ...) {
   ...
}
else {
   if ( ... ) {
      ...
   }
   else {
      if ( ... ) {
         ...
      }
   }
}

~~~

Como siempre, hay que procurar buscar claridad, legibilidad y sencillez en nuestro programa. Si tenemos que anidar sentencias `if`, hacerlas lo más claras y eficientes posibles.

#### Sentencias condicionales en Python

Las estructuras de control de flujo condicionales, se definen mediante el uso de tres palabras claves reservadas, del lenguaje: `if` , `elif` (como el `else-if`de C) y `else`.

Veamos su sintaxis con algunos ejemplos:

~~~python
if semaforo == verde:
    print "Cruzar la calle"
else:
    print "Esperar"
~~~

~~~python
if compra <= 100:
    print "Pago en efectivo"
elif compra > 100 and compra < 300:
    print "Pago con tarjeta de débito"
else:
    print "Pago con tarjeta de crédito"
~~~

~~~python
importe_a_pagar = total_compra
if total_compra > 100:
    tasa_descuento = 10
    importe_descuento = total_compra * tasa_descuento / 100
    importe_a_pagar = total_compra – importe_descuento
~~~

### Operador `?`

Es una herramienta útil para evaluar expresiones condicionales de forma abreviada.

Su **sintaxis** general es la siguiente:

~~~c
expresión1 ? expresión2 : expresión3;
~~~

**Semántica**:

Si la `expresión1` es cierta, entonces se evalúa la `expresión2`, en
otro caso se evalúa la `expresión3`.

Ejemplo:

~~~c
a = b < 0 ? -b : b;

/*
Si el valor de b es menor que 0, la expresión completa tomará el valor de -b, en otro caso tomará el valor de b.
En definitiva, a la variable a se le asigna el valor absoluto de b
dependiendo de la condición b < 0. La sentencia anterior completa
es equivalente a: if (b<0) a = -b; else a = b;
*/
~~~

### Sentencias `switch`

La sentencia `switch`permite seleccionar entre múltiples opciones.

La **sintaxis** de la sentencia `switch`es:

~~~c
switch (variable_entera_a_evaluar) {
   case resultado_a:
      instruccion_a_realizar_resultado_a;
      break;
   case resultado_b:
      instruccion_a_realizar_resultado_b;
      break;
   default :
      instruccion_a_realizar_resultado_diferente_a_b;
}
~~~

La **semántica** de la sentencia `switch`es:

- Se evalúa en primer lugar la expresión que va entre paréntesis a continuación del `switch`. Debe dar como resultado un número entero.
- Después la ejecución empieza en el primer `case` cuya expresión coincida con el resultado obtenido en `variable_entera_a_evaluar`. Se ejecutan todas las instrucciones hasta el `break`.
- El `default`se ejecuta si no ha habido ningún `case`cuyo resultado coincida con `variable_entera_a_evaluar`.
- Si hubiesen dos o más sentencias `case`seguidas sin `break`, se ejecutan todas hasta llegar al `break`.

Diagrama:

<img src="imagenes/switch.png" width="600px"/>

Ejemplo sentencia `switch-case`:

~~~c
int numHermanos = 6; // Prueba a usar 0,1,2,3,4 ...

switch (numHermanos) {
   case 0:      
      printf("Hijo/a único\n");
      break;
   case 1:
      printf("Pareja \n");
      break;
   case 2:
      printf("Familia numerosa \n");
      break;
   default :
        printf("Familia muy numerosa \n");
}
~~~

Cada bloque de sentencias `case`debe terminar con un `break`. Si no es así, el compilador entiende que también debe ejecutarse el bloque del case siguiente y lo engloba como el mismo bloque. Ejemplo:

~~~c
// Sentencias case sin break
// Si contador vale 1 se ejecutarán las dos sentencias `printf`:
switch (contador) {
   case 1:
      printf("Opcion 1");
   case 2:
      printf("Opcion 2");
}
~~~

Lo anterior es equivalente a:

~~~c
switch (contador) {
   case 1:
   case 2:
      printf("Opcion 1");
      printf("Opcion 2");
}
~~~

Ejemplo de enumeraciones y `switch`:

~~~c
enum paloPoker {pica, corazon, trebol, diamante};
enum paloPoker miCarta = pica;switch (miCarta) {
   case diamante:
      printf("Diamante \n");
      break;
   case trebol:
      printf("Trébol \n");
      break;
   case corazon:
      printf("Corazón \n");
      break;
   case pica:
      printf("Pica \n");
      break;
   default :
      printf("La carta no es de poker \n");
}
~~~

Ejemplo con caracteres (internamente se almacenan con un valor entero, su valor ASCII):

~~~c
    char letra;
    printf("Introduzca una letra: ");
    scanf("%c", &letra);
    switch(letra) {
        case 'a':
            printf("Se ha pulsado una a.");
            break;
        case 'e':
            printf("Se ha pulsado una e.");
            break;
        case 'i':
            printf("Se ha pulsado una i.");
            break;
        case 'o':
            printf("Se ha pulsado una o.");
            break;
        case 'u':
            printf("Se ha pulsado una u.");
            break;
        default:
            printf("Otro carácter");
    }
~~~

### Ejercicios

1. Escribe un programa que pida dos números por teclado y nos indique cual es el mayor, cual es el menor o si son iguales.
2. Escribe un programa que pida dos número por teclado y nos diga si uno es múltiplo del otro (divisible).
3. Escribe un programa que pida tres números por teclado y nos diga cuál es el menor.
4. Escribe un programa que pida una nota de 0 a 10 y la muestre en forma de texto: "Suspenso", "Aprobado", "Notable", "Sobresaliente".
5. Escribe un programa que pida dos números por teclado y una de las cuatro operaciones aritméticas de una calculadora (+, -, *, /). Devuelve el resultado de la operación aplicada a los dos números.
6. Escribe un programa que calcule el índice de masa corporal IMC de una persona. Se debe introducir el peso en kg y la altura en m. El IMC = peso / (altura * altura). El programa muestra por pantalla el tipo de peso:
   - IMC < 18.0 --> "Inferior al normal"
   - 18.1 - 24.9 --> "Normal"
   - 25.0 - 29.9 --> "Sobrepeso"
   - IMC > 30.0 --> "Obesidad"
7. Escribe un programa que solicite al usuario una letra (mayúscula o minúscula) e indique si es una vocal o una consonante.

___





## Bibliografía

- Capítulos 5 y 6 de "Programación en C, metodología, algoritmos y estructuras de datos", Luis Joyanes, Ignacio Zahonero
- Capítulos 5.1 a 5.7 de "Fundamentos de Programación", Jesús Carretero y otros  

----

Programación 1, Grado de Robótica, curso 2020-21  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Cristina Pomares Puig
