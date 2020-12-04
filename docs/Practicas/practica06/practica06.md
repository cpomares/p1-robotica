# Práctica 6: Datos estructurados: Registros

**Duración**: 2 semanas

Para la realización de esta práctica vamos a partir del programa de la sopa de letras de la práctica anterior (puedes utilizar como punto de partida tu solución o la publicada por los profesores).

- Debes ampliar las direcciones para ocultar la palabra a las 8 posibles horizontales, verticales y diagonales.

~~~c
typedef enum {IZQUIERDA, DERECHA, ARRIBA, ABAJO, IZQ_ARRIBA, DER_ARRIBA, IZQ_ABAJO, DER_ABAJO} TDireccion;
~~~

- Al ejecutar el programa, se pasará desde línea de comandos un máximo de 5 palabras a ocultar. Las palabras que no quepan en la sopa de letras, se descartarán. Si hay más de 5 palabras válidas, se descartarán las restantes. 
- Se deben ocultar las palabras leídas en la sopa de letras. No hace falta tener en cuenta posibles solapes entre ellas. 
- Se pedirán desde teclado las palabras que ha descubierto el usuario, restringiendo el tiempo a 30 segundos, a partir del cual no se podrá introducir ninguna palabra más. 
- A continuación se mostrará la solución y las palabras que ha acertado el usuario.

Hay que usar las siguientes definiciones, aparte de las de la práctica anterior:

~~~c
typedef struct {
    int fila;
    int columna;
} TPosicion;

typedef struct {
    TCadena   palabra;
    TPosicion  posicion;
    TDireccion direccion;
} TPalabraSopaLetras;

typedef TPalabraSopaLetras TPalabras[MAX_PALABRAS];
~~~

**Observación**:
Es posible que las palabras a ocultar en la sopa de letras se superpongan unas con otras. No lo vamos a tener en cuenta. En el ejemplo 1 no se superponen las palabras, pero en el ejemplo 2 puedes comprobar que después de escribir en la sopa de letras la palabra “francia”, se ha escrito la palabra “suecia”, haciendo desaparecer la primera de ellas.

**Ayuda implementación**: Para calcular cuánto tiempo ha transcurrido entre dos instantes de tiempo determinados, utiliza lo siguiente:

~~~c
time_t  hora_inicio, hora_fin;
double tiempo_transcurrido;

hora_inicio = time(NULL);  // nos devuelve la hora actual

. . .  // sentencias de las que mediremos su tiempo de ejecución

hora_fin = time(NULL);

// calcular los segundos transcurridos entre hora inicio y hora fin
tiempo_transcurrido = difftime(hora_fin, hora_inicio); 
~~~


**Ejemplo 1 de ejecución**: 

Se indican 4 palabras a ocultar, de las cuales una se descarta porque no cabe en la sopa de letras. Después se introducen por teclado 2 palabras encontradas y excedemos el tiempo límite, por lo que no se pueden introducir mas palabras. Las 2 palabras encontradas son respuestas correctas.

~~~text
$ ./programa portugal liechtenstein francia italia

SOPA DE LETRAS

q i c a d w d z j j 
l t p p y v z j q z 
a a f l w f j z c i 
g l a i c n a r f y 
u i n t q f w r g x 
t a j z m s p t x f 
r h v x x g x l g k 
o y q l c w k a b s 
p d h p n w g x e b 
q i z e f m q p j p 

Dispones de 30 segundos para indicar las palabras encontradas...

Introduce una palabra encontrada: portugal
Introduce su posicion inicial (fila columna): 8 0
Introduce dirección
4-IZQ_ARRIBA		2-ARRIBA		5-DER_ARRIBA
0-IZQUIERDA					1-DERECHA
6-IZQ_ABAJO		3-ABAJO		7-DER_ABAJO	...:2

Consumidos 21 segundos

¿quieres introducir otra palabra (s/n): s

Introduce una palabra encontrada: italia
Introduce su posicion inicial (fila columna): 0 1
Introduce dirección
4-IZQ_ARRIBA		2-ARRIBA		5-DER_ARRIBA
0-IZQUIERDA					1-DERECHA
6-IZQ_ABAJO		3-ABAJO		7-DER_ABAJO	...:3

Consumidos 36 segundos

Excedido el tiempo límite para responder


Las palabras ocultas son:

portugal en posición inicial (8,0) y dirección ARRIBA
francia en posición inicial (3,8) y dirección IZQUIERDA
italia en posición inicial (0,1) y dirección ABAJO


Las palabras acertadas son:
portugal
italia
~~~


**Ejemplo 2 de ejecución**: 

Se indican 6 palabras válidas a ocultar y la última se descarta por exceder el límite máximo de palabras. Sólo se introduce por teclado una palabra encontrada, sin consumir el tiempo máximo. La respuesta no es correcta porque la dirección está equivocada.

~~~text
$ ./programa portugal francia italia suiza suecia noruega

SOPA DE LETRAS

n y w p x n z x o i 
o a z i u s z s r y 
l f b n e d m v p p 
k a i a n a r f o c 
c w g c i y e f r a 
h d w u z c o y i o 
t k s n t r e l q i 
d j g k s r a u l u 
q z m z f t o u s e 
i y n z i y b p x v 


Dispones de 30 segundos para indicar las palabras encontradas...

Introduce una palabra encontrada: suiza
Introduce su posicion inicial (fila columna): 1 5
Introduce dirección
4-IZQ_ARRIBA		2-ARRIBA		5-DER_ARRIBA
0-IZQUIERDA					1-DERECHA
6-IZQ_ABAJO		3-ABAJO		7-DER_ABAJO	...:1

Consumidos 16 segundos


¿quieres introducir otra palabra (s/n): n

Consumidos 16 segundos


Las palabras ocultas son:

portugal en posición inicial (9,7) y dirección IZQUIERDA-ARRIBA
francia en posición inicial (3,7) y dirección IZQUIERDA
italia en posición inicial (9,4) y dirección DERECHA-ARRIBA
suiza en posición inicial (1,5) y dirección IZQUIERDA
suecia en posición inicial (8,8) y dirección IZQUIERDA-ARRIBA

No has encontrado ninguna palabra
~~~

----

Programación 1, Grado de Robótica, curso 2020-21  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
