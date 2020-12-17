# Práctica 7: Punteros y memoria dinámica

**Duración**: 2 semanas

Esta práctica consiste en modificar la práctica anterior de forma que se utilice **reserva dinámica de memoria** en lugar de usar reserva estática.

Deberás eliminar las constantes `MAX_PALABRAS`, `NUM_FILAS`, `NUM_COLUMNAS` y `MAX_CADENA`, y reservar sólo la memoria necesaria para las estructuras de datos que utilizaban dichas constantes.

De esta forma, se leerá desde línea de comandos el tamaño de la sopa de letras (filas y columnas) y también un número indeterminado de palabras de cualquier longitud.

**Ejemplo de ejecución**: Se indica desde línea de comandos el tamaño de la sopa de letras (15x20)  y 7 palabras a ocultar, que no se descarta ninguna porque todas caben en la sopa de letras. El funcionamiento del juego es el mismo que en la práctica anterior.

~~~text
$ ./programa 15 20 portugal liechtenstein francia italia suiza suecia noruega

SOPA DE LETRAS

u w s q e z t a e z j m x t b b y e d x 
c s g i t t f x z w t d s v r p l z e j 
x n r d y x z e w t s u e c i a w l s a 
e p k i w v f t n a y t o r e a q z b x 
g h e a v h h b q l a i v c a n g z a d 
f h n a n q t r p c i s h u c f p u i u 
s v o g s t i o d r l t m i y x g m h j 
v l r d v q r c a i a n a r f z e a t u 
o g u n o t c z v n t q y q s e j s t y 
y e e r u x q p a m i l n o f b y y g a 
v p g g o f s z r j m c t k j e r i r r 
p p a g b q i u q q e v h z j o h n a j 
r l b j f u w d s h m b v c a c o r x k 
k m b z s r d m p o e r t e r o s z c u 
j e v v d z v u p l s l b x t s m r h c 

Dispones de 30 segundos para indicar las palabras encontradas...


Introduce una palabra encontrada: italia
Introduce su posicion inicial (fila columna): 9 10
Introduce dirección
4-IZQ_ARRIBA		2-ARRIBA		5-DER_ARRIBA
0-IZQUIERDA					1-DERECHA
6-IZQ_ABAJO		3-ABAJO		7-DER_ABAJO	...:2

Consumidos 25 segundos


¿quieres introducir otra palabra (s/n): s 

Introduce una palabra encontrada: portugal
Introduce su posicion inicial (fila columna): 5 8
Introduce dirección
4-IZQ_ARRIBA		2-ARRIBA		5-DER_ARRIBA
0-IZQUIERDA					1-DERECHA
6-IZQ_ABAJO		3-ABAJO		7-DER_ABAJO	...:6

Consumidos 34 segundos

Excedido el tiempo límite para responder



Las palabras ocultas son:

portugal en posición inicial (5,8) y dirección IZQUIERDA-ABAJO
liechtenstein en posición inicial (1,16) y dirección IZQUIERDA-ABAJO
francia en posición inicial (7,14) y dirección IZQUIERDA
italia en posición inicial (9,10) y dirección ARRIBA
suiza en posición inicial (13,4) y dirección DERECHA-ARRIBA
suecia en posición inicial (2,10) y dirección DERECHA
noruega en posición inicial (5,2) y dirección ABAJO

Las palabras acertadas son:
italia
portugal
~~~

----

Programación 1, Grado de Robótica, curso 2020-21  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
