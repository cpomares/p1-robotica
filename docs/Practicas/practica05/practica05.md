# Práctica 5: Datos estructurados: Arrays

**Duración**: 2 semanas

### Ejercicio 1 ###

Modifica el ejercicio 1 de la práctica 4 para almacenar los intervalos en arrays que como máximo tendrán 20 elementos.

Utiliza la siguiente definición:

~~~c
#define MAX 20
typedef int TIntervalo[MAX];
~~~

Y los siguientes prototipos:

~~~c
void leerIntervalo(int, int*, int*);
int almacenaIntervalo(TIntervalo, int, int);  // almacena un intervalo en un array
void intercalar(TIntervalo, int, TIntervalo, int); // intercala dos arrays de intervalos
void imprimirIntervalo(TIntervalo, int, int); // imprime un array de intervalo
~~~

Si un intervalo es mayor que `MAX`, sólo se almacenarán en el array los valores que quepan.

**Ejemplo de ejecución:**

~~~text
Introduce valores del intervalo 1: 2 7
Introduce valores del intervalo 2: 20 37
2 20 3 21 4 22 5 23 6 24 7 25 26 27 28 29 30 31 32 33 34 35 36 37
~~~

Datos de entrada: `2 intervalos válidos`

**Casos de prueba:**

~~~text
Introduce valores del intervalo 1: 1 25
Introduce valores del intervalo 2: 3 9
1 3 2 4 3 5 4 6 5 7 6 8 7 9 8 9 10 11 12 13 14 15 16 17 18 19 20
~~~

~~~text
Introduce valores del intervalo 1: 9 3
Introduce valores del intervalo 1: 3 9
Introduce valores del intervalo 2: 1 45
3 1 4 2 5 3 6 4 7 5 8 6 9 7 8 9 10 11 12 13 14 15 16 17 18 19 20
~~~

### Ejercicio 2 ###

Implementa la función `concatena` que recibe dos cadenas como parámetro y concatena la segunda a continuación de la primera. No puedes usar las funciones predefinidas `strcat` ni `strlen`. 

**Ejemplo de ejecución:**

~~~text
Introduce cadenas: hola amigo
Resultado: holaamigo
~~~

Datos de entrada: `dos cadenas de texto`

**Casos de prueba:**

~~~text
Datose entrada:
cadena1: hola
cadena2: amigo
Resultado:
cadena1: holaamigo
~~~

~~~text
Datos entrada:
cadena1: AAAAAAAAA
cadena2: BBBBBBBB
Resultado:
cadena1: AAAAAAAAABBBBBBBB
~~~

### Ejercicio 3 ###

Modifica el ejercicio 2 de la práctica 4 para que el calendario se almacene en una matriz de enteros 6x7 (define para ello un tipo `TCalendario`), rellenando con ceros los días vacíos.

El programa tiene que funcionar igual que el de la práctica anterior, pero ahora el calendario se imprime directamente desde los datos almacenados en la matriz. Los 0s almacenados se imprimen como puntos `.`.

Por ejemplo, Octubre 2019 se almacenaría en la siguiente matriz `TCalendario`:

<img src="imagenes/octubre2019.png" width="300px"/>

**Ejemplo de ejecución:**

~~~text
Introduce mes: 10
Introduce año: 2019

 LUN MAR MIE JUE VIE SAB DOM
   .   1   2   3   4   5   6
   7   8   9  10  11  12  13
  14  15  16  17  18  19  20
  21  22  23  24  25  26  27
  28  29  30  31   .   .   .
   .   .   .   .   .   .   .
~~~

~~~text
Introduce mes: 09
Introduce año: 2019

 LUN MAR MIE JUE VIE SAB DOM
   .   .   .   .   .   .   1
   2   3   4   5   6   7   8
   9  10  11  12  13  14  15
  16  17  18  19  20  21  22
  23  24  25  26  27  28  29
  30   .   .   .   .   .   .
~~~

### Ejercicio 4 ###

Basándonos en el programa implementado del ejercicio 3 de la práctica 4, implementa un nuevo programa que pida y valide un número binario de 8 bits y lo dibuje en pantalla con un determinado alto y ancho que habrá sido solicitado previamente. Si algún carácter introducido no es un dígito binario, el programa terminará.

El número binario de 8 bits se debe leer carácter a carácter y almacenarse en un array de caracteres (lo llamaremos `TPalabra`).

Fíjate en los siguiente ejemplos que el carácter de fondo utilizado en lugar de ‘.’ debe ser el carácter que representa un espacio en blanco.


**Ejemplo de ejecución:**

~~~text
Introduce alto [15..30] y ancho [8..20] de los números: 15 8
Introduce palabra de 8 bits: 10010101

   #         ########     ########        #         ########        #         ########        #    
  ##         #      #     #      #       ##         #      #       ##         #      #       ##    
 # #         #      #     #      #      # #         #      #      # #         #      #      # #    
#  #         #      #     #      #     #  #         #      #     #  #         #      #     #  #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         #      #     #      #        #         #      #        #         #      #        #    
   #         ########     ########        #         ########        #         ########        #    

Introduce palabra de 8 bits: 00101011

########     ########        #         ########        #         ########        #            #    
#      #     #      #       ##         #      #       ##         #      #       ##           ##    
#      #     #      #      # #         #      #      # #         #      #      # #          # #    
#      #     #      #     #  #         #      #     #  #         #      #     #  #         #  #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
#      #     #      #        #         #      #        #         #      #        #            #    
########     ########        #         ########        #         ########        #            #    

Introduce palabra de 8 bits: f
Fin del programa
~~~


### Ejercicio 5 ###

Implementa un programa que pida 2 números binarios e imprima su suma binaria. Para ello, ten en cuenta lo siguiente:

- Lee los números carácter a carácter y guárdalos en un array de caracteres.
- La longitud máxima de los números debe ser de 8 bits.
- En el caso de que uno de los números introducidos tenga mayor longitud o no sea binario, el programa terminará.
- Los números introducidos pueden tener distinto tamaño, en cuyo caso habrá que rellenar el menor de ellos con ceros a su izquierda, para que ambos tengan el mismo número de bits.
- La suma binaria se lleva a cabo de la siguiente manera:

    ~~~text
      0 + 0 = 0
      0 + 1 = 1
      1 + 0 = 1
      1 + 1 = 0  y acarreo 1
    ~~~


**Ejemplo de ejecución:**

~~~text
Introduce palabra de máximo de 8 bits: 11
Introduce palabra de máximo de 8 bits: 11


     11
   + 11
     --
    110
Introduce palabra de máximo de 8 bits: 111
Introduce palabra de máximo de 8 bits: 11


     111
   + 011
     ---
    1010
Introduce palabra de máximo de 8 bits: 00011
Introduce palabra de máximo de 8 bits: 101


     00011
   + 00101
     -----
     01000
Introduce palabra de máximo de 8 bits: 11111111
Introduce palabra de máximo de 8 bits: 10010100


     11111111
   + 10010100
     --------
    110010011
Introduce palabra de máximo de 8 bits: f
Fin del programa
~~~


----

Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
