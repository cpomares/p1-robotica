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

Escribe un programa que calcule el sueldo de un trabajador de una empresa que cobra 50.000€ anuales, en base a los siguientes criterios:

- Si lleva más de 10 años en la empresa se le aplica un aumento del 10%.
- Si lleva menos de 10 años pero 5 o más años se le aplica un aumento del 7%.
- Si lleva menos de 5 años pero 3 o más años se le aplica un aumento del 5%.
- Si lleva menos de 3 años se le aplica un aumento del 3%.

Ejemplo de ejecución:

~~~text
Introduzca la antigüedad del trabajador: 15
El aumento que le corresponde al trabajador es de 5000.00€
Su sueldo quedará en: 55000.00€
~~~

Datos de entrada: `años`

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
|  15              |  5000 55000  |
|  3               |  2500 52500  |
|  1               |  1500 51500   |


### Ejercicio 3 ###

Escribe un programa que solicite por teclado una figura:

~~~text
0-Cuadrado
1-Circulo
2-Triangulo
~~~

Y calcule e imprima su perímetro correspondiente. Se deberá solicitar los datos necesarios de cada figura. 

Utiliza `typedef` para definir un tipo enumerado llamado `TFigura` que contenga los identificadores `Cuadrado`, `Circulo` y `Triangulo`. El tipo `TFigura` puedes hacerlo fuera del `main` de forma global. Para leer un tipo enumerado con `scanf` debes poner el formato `%u`, ya que se trata de un entero sin signo.

Datos de entrada:

~~~text
Cuadrado: diámetro (ancho)
Circulo: ancho (base) y alto
Triángulo: lado (ancho)
~~~

Ejemplo de ejecución:

~~~text
0-Cuadrado
1-Circulo
2-Triangulo
Introduce figura:
0
Introduce uno de los lados del cuadrado: 23
El perímetro es: 92.00
~~~

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| 0 23             | El perímetro es: 92.00  |
| 1 100            | El perímetro es: 314.16 |
| 2 20 42 34       | El perímetro es: 96.00  |


### Ejercicio 4 ###

Escribe un programa que pida un número de 4 cifras y lo redondee a la decena y/o centena más próxima. Ten en cuenta que el redondeo a la alza se produce cuando el siguiente dígito es mayor que 5.

En primer lugar debes descomponer el número para obtener sus 4 cifras utilizando los operadores % y / (esto se hace de forma eficiente con un bucle, pero todavía no los hemos visto, así que hazlo de cifra en cifra). 

Ejemplo de ejecución:

~~~text
Introduce número de 4 cifras: 1247
El número redondeado es: 1250
~~~

Datos entrada: número de 4 cifras

Casos de prueba:

| Datos de entrada | Salida por pantalla |      
|:----------------:|:-------------------:|
| 2962             | 2962  |
| 1247            | 1250 |
| 1258       | 1300  |
| 1887.      | 1900 |
| 1847       | 1850 |
| 1486       | 1500 |

----

Programación 1, Grado de Robótica, curso 2020-21  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
