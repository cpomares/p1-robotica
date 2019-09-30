# Práctica 3: Sentencias de iteración

### Ejercicio 1 ###

Escribe un programa que invierta los dígitos de un entero positivo solicitado por teclado (hay que validar el dato) y lo almacene en una variable. La variable que contiene el número invertido se mostrará por pantalla posteriormente.

**Ejemplo de ejecución:**

~~~text
Introduce un numero positivo:123456
El número invertido es: 654321
~~~

Datos de entrada:  `número positivo`

**Casos de prueba:**

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
|  -321            | se vuelve a solicitar |
|  123456          | 654321   |   
|  21334111        | 11143312 |   
|  1               | 1        |


### Ejercicio 2 ###

Implementa un programa que calcule el resultado acumulado de aplicar sucesivas operaciones aritméticas. El programa inicialmente solicitará un número entero y a continuación irá solicitando un operador aritmético y el siguiente operando, acumulando el resultado para la siguiente operación. 

Los operadores aritméticos permitidos serán ‘+’, ‘-‘, ‘*’, ‘/‘. En caso de introducir un operador incorrecto, se volverá a pedir. El programa deberá terminar cuando el carácter introducido como operador sea un punto ‘.’
Hay que tener en cuenta que no se puede hacer una división por cero, en cuyo caso se mostrará el mensaje “Error: división por cero” y se solicitará la siguiente operación a realizar.

**Ejemplo de ejecución:**

~~~text
Introduce un número: 4
Introduce operador aritmético ('.' para terminar): +
Introduce un número: 6
El resultado parcial acumulado es: 10
Introduce operador aritmético ('.' para terminar): /
Introduce un número: 5
El resultado parcial acumulado es: 2
Introduce operador aritmético ('.' para terminar): .
El resultado final acumulado es: 2
~~~

**Casos de prueba:**

- Datos de entrada: `25 .`
- Resultado esperado (salida por pantalla): 

    ~~~text
    Introduce un número: 25
    Introduce operador aritmético ('.' para terminar): .
    El resultado final acumulado es: 25
    ~~~
    
- Datos de entrada: `34 - 14 / 0 .`
- Resultado esperado (salida por pantalla): 

    ~~~text
    Introduce un número: 34
    Introduce operador aritmético ('.' para terminar): -
    Introduce un número: 14
    El resultado parcial acumulado es: 20
    Introduce operador aritmético ('.' para terminar): %
    Introduce operador aritmético ('.' para terminar): /
    Introduce un número: 0
    Error: división por cero
    El resultado parcial acumulado es: 20
    Introduce operador aritmético ('.' para terminar): .
    El resultado final acumulado es: 20
    ~~~

### Ejercicio 3 ###

Escribe un programa que pida un número positivo e impar (hay que validar el dato), y en base a él imprima la figura que se indica en el ejemplo. El número máximo de columnas siempre es fijo: 4.

**Ejemplo de ejecución:**

~~~text
Introduce un número: 7
1
1       2
1       2       3
1       2       3       4
1       2       3
1       2
1
~~~

Datos de entrada: `número impar`

**Casos de prueba:**

- Datos de entrada: `5`
- Resultado esperado (salida por pantalla): 

    ~~~text
    Introduce un número: 5
    1
    1       2
    1       2       3
    1       2
    1
    ~~~
    
- Datos de entrada: `9`
- Resultado esperado (salida por pantalla): 

    ~~~text
    Introduce un número: 9
    1
    1       2
    1       2       3
    1       2       3       4
    1       2       3       4
    1       2       3       4
    1       2       3
    1       2
    1
    ~~~


### Ejercicio 4 ###

Implementa un programa que dibuje en pantalla el número 10 con un alto y ancho especificado. Inicialmente se pedirá el alto y ancho cuyos valores deben están incluidos en los intervalos [15..30] y [8..20] respectivamente. Se validarán dichos valores introducidos y cuando sean correctos, se procederá a dibujar el número 10. 
Utilizaremos ‘#’ como carácter de relleno, y ‘.’ como carácter de fondo (en vez de usar el carácter blanco ‘ ‘).
Los dos dígitos estarán espaciados por 5 caracteres.
Para dibujar la diagonal del número 1, usaremos la mitad del ancho especificado.


**Ejemplo de ejecución:**

~~~text
Introduce alto [15..30] y ancho [8..20] de los números: 15 10
....#.....##########
...##.....#........#
..#.#.....#........#
.#..#.....#........#
#...#.....#........#
....#.....#........#
....#.....#........#
....#.....#........#
....#.....#........#
....#.....#........#
....#.....#........#
....#.....#........#
....#.....#........#
....#.....#........#
....#.....##########

~~~

Datos de entrada: `dos números enteros`

**Casos de prueba:**

- Datos de entrada: `20 5` `20 8`
- Resultado esperado (salida por pantalla): 

    ~~~text
    Introduce alto [15..30] y ancho [8..20] de los números: 20 5
    Introduce alto [15..30] y ancho [8..20] de los números: 20 8
    ...#.....########
    ..##.....#......#
    .#.#.....#......#
    #..#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....#......#
    ...#.....########
    ~~~

- Datos de entrada: `15 20`
- Resultado esperado (salida por pantalla): 

    ~~~text
    Introduce alto [15..30] y ancho [8..20] de los números: 15  20
    .........#.....####################
    ........##.....#..................#
    .......#.#.....#..................#
    ......#..#.....#..................#
    .....#...#.....#..................#
    ....#....#.....#..................#
    ...#.....#.....#..................#
    ..#......#.....#..................#
    .#.......#.....#..................#
    #........#.....#..................#
    .........#.....#..................#
    .........#.....#..................#
    .........#.....#..................#
    .........#.....#..................#
    .........#.....####################
~~~

----

Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
