# Práctica 8: Entrada y salida

**Duración**: 2 semanas

## Ejercicio

Implementa un programa que lea un fichero de texto y escriba en otro fichero de texto las palabras en orden inverso.

Ejemplo: Si en el fichero original de entrada tenemos el siguiente texto:

~~~text
Esto es una frase de prueba para el ejercicio de invertir el orden de las palabras de un fichero de texto.
Y esta otra frase está en otro párrafo.
~~~

El programa deberá generar el siguiente fichero de texto de salida:

~~~text
párrafo.
otro en está frase otra esta Y texto.
de fichero un de palabras las de orden el invertir de ejercicio el para prueba de frase una es Esto
~~~

Si volviésemos a ejecutar el programa pasando como argumento el fichero de salida, se debería volver a generar un fichero igual que el original.

El programa deberá recibir un argumento desde línea de comandos con el nombre del fichero de entrada (con extensión .txt) y leer (carácter a carácter con `fgetc`) todas sus palabras guardándolas en un array dinámico de cadenas de caracteres, que a su vez también se crearán con reserva de memoria dinámica. Después deberá escribir en otro fichero de texto las palabras almacenadas en el array dinámico en orden inverso.

Suponemos que las palabras están separadas por un espacio en blanco y para mantener los distintos párrafos, incluye el carácter final de línea en la última palabra de cada párrafo.

Deberás construir el nombre del fichero de salida de la siguiente forma:
nombre original (sin extensión) + "_out" + extension.

Por ejemplo, si el fichero de entrada se denomina `"prueba.txt"`, el fichero de salida tendrá el nombre: `"prueba_out.txt"`.

Además, debes implementar versiones de las funciones `strcpy()`, `strncpy()` y `strcat()` para que trabajen con memoria dinámica. Las funciones de librería `strcpy`y `strcat`ya las conoces. La función de librería `strncpy` copia los `n` primeros caracteres de una cadena en otra, por ejemplo:

~~~c
...
strncpy(texto2, texto1, 4);
texto2[4]='\0';
printf("Los 4 primeros caracteres son %s\n", texto2);
~~~

Define las nuevas funciones con los siguientes prototipos:

~~~c
TCadena strcpyDinamico(TCadena);
TCadena strncpyDinamico(TCadena, int);
void    strcatDinamico(TCadena*, TCadena);
~~~

Finalmente, debes utilizar las siguientes definiciones de tipos de datos:

~~~c
typedef char* TCadena;

typedef struct {
    int n;
    TCadena* palabras;
} TTexto;
~~~

----

Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Antonio Botía, Cristina Pomares
