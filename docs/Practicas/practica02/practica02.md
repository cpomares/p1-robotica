# Práctica 2: Sentencias de selección

### Ejercicio 1 ###

Implementa un programa que solicite un carácter e imprima un mensaje que indique qué tipo de carácter es, teniendo en cuenta que el programa debe reconocer caracteres de tipo dígito, letras minúsculas y letras mayúsculas. Ante cualquier otro tipo de carácter, el programa indicará que es desconocido.

Ejemplo de ejecución:

~~~text
Introduce un carácter: a
El carácter introducido es una letra minúscula
~~~

Datos de entrada: `un carácter`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| a                | El carácter introducido es una letra minúscula |
| 4                | El carácter introducido es un dígito          |   
| %                | El carácter introducido es desconocido     |   
| F                | El carácter introducido es una letra mayúscula | 


### Ejercicio 2 ###

Escribe un programa que indique el número de días que tiene un mes suponiendo que el año no es bisiesto. El usuario debe introducir un número de mes por teclado (0-enero, 11-diciembre) y suponemos que siempre se introduce un número correcto. El programa debe imprimir por pantalla el número de días que tiene ese mes.

Utiliza `typedef` para definir un enumerado `TMeses`, puedes hacerlo fuera del `main` de forma global.

Ejemplo de ejecución:

~~~text
Introduce número de un mes 0 (enero), 11 (diciembre):
3
El mes número 3 tiene 31 días
~~~

Dato de entrada: `número de mes 0-11`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| 3                | El mes número 3 tiene 30 días  |
| 11               | El mes número 11 tiene 31 días |
| 2                | El mes número 2 tiene 28 días  |

### Ejercicio 3 ###

Utilizando el tipo enumerado `TipoFigura` del ejercicio 5 de la práctica anterior, escribe un programa que solicite por teclado una de las tres figuras y calcule e imprima su área correspondiente. Para ellos deberá solicitar los datos necesarios de cada figura. 

Utiliza `typedef` para definir el enumerado `TipoFigura`, puedes hacerlo fuera del main de forma global.

Ejemplos de ejecución:

~~~text
1-Circulo
2-Triangulo
3-Cuadrado
Introduce figura:
1
Introduce diámetro (ancho) del círculo: 30
El area es: 94.20
~~~

Datos de entrada: `tipo figura`, `ancho`, `[alto]`

- `Círculo`, `ancho` 
- `Triángulo`, `ancho`, `alto`
- `Cuadrado`, `ancho`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| 1 30             | El área es: 94.20   |
| 2 23 30          | El área es: 345.00  |
| 3 20             | El área es: 400.00  |


### Ejercicio 4 ###

Implementa un programa que calcule la nota final de la asignatura. En primer lugar se debe solicitar la convocatoria, `'E'` si se trata de la de Enero o `'J'` si se trata de Julio. Si no se teclea ninguna de ellas, se mostrará un mensaje en el que se indique que es incorrecta. 

La nota final de la convocatoria de Enero se calcula tal y como está explicado en el ejercicio 4 de la práctica 1.La nota final de la convocatoria de Julio consiste en un único examen.

Además de la nota numérica, deberá aparecer su descripción literal equivalente, teniendo en cuenta:

- `0 <= nota < 5` ==> SUSPENSO
- `5 <= nota < 7` ==> APROBADO
- `7 <= nota < 9` ==> NOTABLE
- `nota >= 9` ==> SOBRESALIENTE 

Ejemplo de ejecución:

~~~text
Dime la convocatoria(E,J):E
Introduce la nota del primer examen (temas 1 al 3): 7.3
Introduce la nota del segundo examen (temas 1 al 6): 8.4
Introduce la nota del tercer examen (temas 1 al 9): 6.5
La nota final en la asignatura es: 7.28  NOTABLE
~~~

Datos de entrada: `convocatoria`, `nota1`, `[nota2]`, `[nota3]`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| E 7.3 8.4 6.5    | La nota final en la asignatura es: 7.28  NOTABLE |
| J 9.3            | La nota final en la asignatura es: 9.30  SOBRESALIENTE |
| E 4.5 3.7 2.5.   | La nota final en la asignatura es: 3.22  SUSPENSO |
| x                | La convocatoria introducida es incorrecta |


----

Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
