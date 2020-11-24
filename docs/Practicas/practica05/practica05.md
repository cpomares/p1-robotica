# Práctica 5: Datos estructurados: Arrays

**Duración**: 2 semanas

### Ejercicio 1 ###

Implementa un programa que compruebe los aciertos que tiene una quiniela de futbol. 

Una quiniela está formada por 8 apuestas, y cada apuesta contiene los resultados (1, X, 2) de 14 partidos de futbol. El pleno al 15 no lo tendremos en cuenta.

Los resultados de la quiniela completa (las 8 apuestas) se rellenarán de forma aleatoria y también se generará de forma aleatoria los resultados reales (1, X, 2) de los partidos.

Una vez generados todos estos resultados aleatorios, el programa mostrará la quiniela completa y los resultados reales de los partidos, y finalmente deberá calcular y mostrar los aciertos de cada apuesta e indicar cuál ha sido la ganadora.
En el caso de que varias apuestas tengan los mismos aciertos, se mostrará como ganadora la primera de ellas.

La implementación de este ejercicio hazla **sin** utilizar `typedef` para las matrices / arrays.

**Ejemplo de ejecución:**

~~~text

		APUESTAS QUINIELA				RESULTADOS
--------------------------------------------------------
2	X	X	X	X	X	1	2			1
--------------------------------------------------------
2	2	X	2	X	X	1	X			X
--------------------------------------------------------
1	1	1	X	X	1	1	2			1
--------------------------------------------------------
X	X	2	1	2	X	X	1			X
--------------------------------------------------------
X	1	2	1	2	2	1	X			1
--------------------------------------------------------
X	1	X	X	X	2	1	2			1
--------------------------------------------------------
X	2	1	2	2	1	X	1			1
--------------------------------------------------------
1	2	1	1	1	1	2	X			1
--------------------------------------------------------
X	1	2	1	2	X	2	1			X
--------------------------------------------------------
X	X	X	2	2	1	X	X			1
--------------------------------------------------------
1	1	2	1	X	X	2	2			X
--------------------------------------------------------
1	X	2	1	1	1	2	1			1
--------------------------------------------------------
1	2	2	1	1	X	X	2			X
--------------------------------------------------------
2	1	1	2	2	2	X	1			1
--------------------------------------------------------

Aciertos:
5	5	5	3	4	10	6	4
	
La apuesta 6 ha sido la ganadora!!!!
~~~

### Ejercicio 2 ###

Implementa un programa que muestre una sopa de letras con una palabra escondida.

El programa debe generar una sopa de letras de tamaño 10x10, que estará formado por letras minúsculas seleccionadas aleatoriamente.

A continuación pedirá por teclado una palabra, de un tamaño que quepa dentro de la sopa de letras. La posición inicial de la palabra dentro de la sopa de letras se seleccionará de forma aleatoria, así como la dirección en la que se escribirá. Las direcciones válidas son izquierda y derecha en sentido horizontal, y también se elegirán de forma aleatoria.

El programa a continuación mostrará la sopa de letras con la palabra escondida, y el usuario deberá descubrirla en un tiempo máximo que se irá mostrando en pantalla en forma de una cuenta atrás. Una vez finalizada la cuenta atrás, se mostrará la solución.

**Ejemplo de ejecución:**

~~~text
Introduce palabra de máxima longitud 10: asignaturas
Introduce palabra de máxima longitud 10: hola

SOPA DE LETRAS

g b f l i a l o h r 
b a l k x d l s m l 
x h k c v t w i m x 
l r l s u t u g g s 
x a w d v k s p i n 
n o t g h r r q y w 
v j p s j e l d g f 
a o g w t r r n d r 
o r g f d g q p v s 
i x v e r g z s q y 


Cuenta atrás...
10 9 8 7 6 5 4 3 2 1 

La palabra "hola" se encuentra en la posición inicial (0, 8) en dirección IZQUIERDA
~~~


Debes utilizar, al menos, las siguientes definiciones en tu programa:

~~~c
#define NUM_FILAS 10
#define NUM_COLUMNAS 10
#define MAX_CADENA 80

typedef char TSopaLetras[NUM_FILAS][NUM_COLUMNAS];
typedef char TPalabra[MAX_CADENA];
~~~

Te damos la implementación de las siguientes funciones:

~~~c
// Esta función genera de forma aleatoria una letra minúscula, 
// teniendo en cuenta que el código ASCII tiene 26 letras minúsculas
char LetraAleatoria() {
    char letra;
    int  num;
    
    num = rand() % NUM_LETRAS;
    letra = 'a' + num;
 
    return letra;
}



// Esta función imprime en pantalla una cuenta atrás, segundo a segundo
// Hay que incluir : #include <unistd.h>
void CuentaAtras() {
    int i;
    
    printf("\nCuenta atrás...\n");
    for (i=SEGUNDOS_CUENTA_ATRAS; i>0; i--) {
        printf("%d ", i);
        fflush(stdout);
        sleep(1);
    }
}
~~~

----

Programación 1, Grado de Robótica, curso 2020-21  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
