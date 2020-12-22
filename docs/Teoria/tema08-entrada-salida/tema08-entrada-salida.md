
# Tema 8: Entrada / salida

## 1. Introducción

C ofrece un conjunto de funciones para realizar operaciones de entrada y salida (E/S) con las cuales puedes leer y escribir cualquier tipo de fichero.

El manejo de archivos en C se hace mediante el concepto de flujo (*streams*) o canal. Los flujos pueden estar abiertos o cerrados, y conducen los datos entre el programa y los dispositivos externos.

### 1.1 Ficheros

- Toda la información manejada hasta ahora se pierde cuando termina la ejecución de un programa, tanto la introducida como la generada.- Si tenemos que manejar una gran cantidad de información (un número elevado de variables, valores, etc.) no parece razonable definir esa información en el código.- Además, puede que la información a tratar no la tengamos, sino que queramos procesar información que nos suministran almacenada.- Un fichero almacena de manera permanente la información, usando la memoria permanente (disco duro) del ordenador.- Para C todo en el ordenador es un fichero: teclado, impresora, cualquier otro dispositivo conectado al ordenador.


### 1.2 *Streams* (flujos) de E/S

Un *stream* (flujo) es una abstracción que se refiere a un conjunto de datos que fluye entre un origen y un destino. Entre el origen y el destino debe existir una conexión o canal (*pipe*) por el que circulen los datos.

Cuando se crea o abre un fichero, se crea un ***stream*** asociado al fichero, y se genera un descriptor de archivo para poder identificarlo.

Además, se crea un ***buffer*** (almacén intermedio) por donde pasan los datos del archivo. Se utiliza para optimizar las lecturas y escrituras, sobre todo si se realizan de pocos datos y de forma continua.

Se puede pensar en el buffer como un array donde se van almacenando los datos dirigidos al archivo o desde el archivo. El buffer se vuelca cuando de una forma u otra se da la orden de vaciarlo.

Todo archivo abierto lleva asociado un puntero de posición que indica el lugar donde realizará la siguiente lectura o escritura. Cuando se crea un archivo, el **puntero de la posición** es cero (inicio). Se va actualizando conforme se lee o se escribe. Se puede indicar una nueva posición con la función *fseek*.

Hay dos tipos de *streams*:

- Uno es el *stream* de **texto**, consistente en líneas de texto. Una línea es una secuencia de caracteres terminada en el carácter de línea nueva ('\n' ó '\r\n').
- El otro formato es el del *stream* **binario**, que consiste en una secuencia de bytes que representan datos internos como números, estructuras o arrays. Se utiliza principalmente para datos que no son de tipo texto, pueden contener cualquier información. La codificación de estos ficheros ha de estar especificada mediante un estándar o con la documentación del programa.

En el momento de abrir o crear un *stream*, hay que indicar de qué tipo de archivo se trata:

- **Texto**. Formado por líneas de caracteres, terminadas en un salto de línea.
- **Binario**. Formado por una secuencia ordenada de caracteres, sin separadores especiales, que pueden almacenar cualquier tipo de información.

No hay diferencia real entre uno y otro, salvo que en un fichero en modo texto hay fines de línea y hay funciones de ficheros que pueden buscarlos. Si se abre en modo binario, la información puede ser de cualquier tipo y las funciones de ficheros no buscarán fines de línea.


## 2. Manejo de ficheros

Cuando trabajamos con ficheros se suele usar el mismo esquema, tanto si escribimos como si leemos:- Abrir el fichero- Comprobar si el fichero está abierto- Si está abierto, leer/escribir en él hasta que se encuentra el fin de fichero- Cerrar el fichero

### `FILE*`

`FILE*` es la estructura que representa un archivo y se encuentra en la cabecera `stdio.h`. Esta estructura contiene información sobre el archivo, como la dirección del *buffer*, el modo de apertura,el último carácter leído, o el indicador de posición de fichero.  
Los campos de `FILE*`pueden cambiar de un compilador a otro.

Ejemplo:

~~~c
FILE *ptr_fich;
FILE *mostrar();  // prototipo de función
~~~


### 2.1 Abrir el fichero

Para trabajar con un archivo, la primera operación que hay que realizar es abrirlo. La apertura conecta el archivo externo con el programa, y hay que indicarle cómo se va a tratar: binario, de caracteres. etc. El programa accede a los archivos a través de `FILE*`, la función de apertura devuelve dicho puntero.

La función `fopen` abre o crea un fichero:
Sintaxis:

~~~c
FILE* fopen(char *nombre, char *modo)
~~~

Los parámetros que recibe `fopen` son:- `nombre`: cadena de caracteres con la ruta del fichero a abrir- `modo`: cadena de caracteres que indica cómo vamos a abrir el fichero. Lo veremos más adelante.

La función `fopen` devuelve un puntero de tipo `FILE`. Si ha ocurrido algún error al abrirse, devuelve NULL.

El parámetro `modo` es una combinación de los caracteres r (read, lectura), w (write, escritura), b (binario), a (append, añadir), y + (actualizar).

~~~c
#include <stdio.h>
#include <stdlib.h>

int main() {
   FILE *f;
   char name[] = "notas.txt";

   f = fopen(name, "r");
   if (f == NULL) {
      printf("Error al abrir el archivo\n");
   }
   else {
      // Archivo abierto con éxito
   }

~~~

#### Modos de apertura de un archivo

El segundo parámetro de `fopen`indica el modo de tratar el archivo: lectura, escritura, añadido, texto o binario.

Por defecto siempre el archivo es de texto. Se utiliza la letra `b`para modo binario como último carácter. Algunos compiladores admiten la letra `t`al final para archivos de texto.

- **"r"** modo lectura. El flujo se posiciona al principio del fichero.
- **"r+"** modo lectura y escritura. El flujo se posiciona al principio del fichero- **"w"** modo escritura. Si el fichero no existe, se crea. Si existe, se trunca a 0. El flujo se posiciona al principio del fichero- **"w+"** modo lectura y escritura. Si el fichero no existe, se crea. Si existe, se trunca a 0. El flujo se posiciona al principio del fichero
- **"a"** modo escritura añadir al final. Si el fichero no existe, se crea. El flujo se posiciona al final del fichero.- **"a+"** modo lectura y escritura añadir al final. Si el fichero no existe, se crea. El flujo se posiciona al final del fichero.
- Podemos combinar modos: **"rw"**

Para abrir un archivo binario:

    "rb", "wb", "ab", "r+b", "w+b", "a+b"

Ejemplo: Tenemos un archivo de texto de lectura "licencia,txt" y queremos grabar los datos procesados en un archivo binario "resumen.dat". Las operaciones de apertura son:

~~~c
int main() {
   FILE *pf1, *pf2;
   char org[] = "licencia.txt";
   char dest[] = "resumen.dat";

   pf1 = fopen(org, "r");
   pf2 = fopen(dest, "wb");
   if (fp1 == NULL || fp2 == NULL) {
      // Error
   }
}
~~~

### 2.2 Cerrar un fichero

Los archivos en C trabajan con una memoria intermedia llamada *buffer*. La entrada y salida de datos se almacena en ese *buffer*, volcándose cuando está lleno.
Siempre que se termina de trabajar con un fichero y siempre que se termine la ejecución de un programa, hay que cerrar los ficheros abiertos para que, entre otras cosas, se vuelque el *buffer* y no queden datos sin actualizar.

La función `fclose` cierra un fichero.

~~~c
int fclose(FILE *f)
~~~

- La función devuelve 0 si se cerró con éxito- Cuando se termina la ejecución de un programa, el sistema operativo se "suele" encargar de cerrar todos los ficheros abiertos- Si no cerramos los ficheros abiertos podemos tener problemas.

Ejemplo:

~~~c
FILE *f1, *f2;

f1 = fopen("datos.txt", "r");
f2 = fopen("arbol.txt", "w");

fclose(f1);
fclose(f2);
~~~


### 2.3 Funciones de entrada y salida para ficheros

- La estructura `FILE` contiene una posición (marca) de por dónde vamos leyendo en el fichero.- Si leemos algo del fichero, la marca avanza hasta el siguiente carácter/dato disponible.- Si volvemos a leer del fichero, leemos a partir de la marca.- Para saber si hemos llegado al final del fichero, usaremos la función `feof (FILE *f)` (devuelve 0 si no se ha encontrado).


#### Funciones de entrada y salida de caracteres: `fgetc`y `fputc`

`fputc`escribe un carácter en el archivo asociado con el puntero a `FILE`. Devuelve `EOF`si no puede escribirse. Si todo es correcto, avanza el puntero de posición.

~~~c
int fputc (int carácter, FILE *f)
~~~

Ejemplo: Lee caracteres desde teclado hasta introducir la 'Z', y los va grabando uno a uno en el fichero:

~~~c
int main() {
   char c;
   FILE *f;
   char salida[] = "salida.txt";

   if ((f = fopen(salida,"w")) == NULL)
      printf("Error en la apertura del fichero");
   else {
      do {
         scanf("\n%c", &c);
         fputc(c, f);
      } while (c != 'Z');
      fclose(f);
   }
}
~~~

`fgetc` devuelve el carácter siguiente del archivo (*stream*). Devuelve el carácter `EOF` si hemos llegado al final del fichero.

Sintaxis:

~~~c
int fgetc (FILE *f)
~~~

Ejemplo: Imprime por pantalla el contenido del fichero carácter a carácter y el número de líneas que contiene:

~~~c
int main() {
   int c, n = 0;
   FILE *f;
   char salida[] = "salida.txt";

   if ((f = fopen(salida,"r")) == NULL)
      printf("Error en la apertura del fichero");
   else {
      while ((c = fgetc(f)) != EOF){
         if (c == '\n') {
            n++;
            printf("\n");
         } else
            printf("%c", c);
      }
      printf("Número de líneas del archivo: %d", n);
      fclose(f);
   }
}
~~~

Ejemplo con `fputc`y `fgetc`:

~~~c
int main() {
   FILE *f1, *f2;
   char ch;

   f1 = fopen("file1.txt","r");
   f2 = fopen("file2.txt","w");

   if (f1 == NULL) {
      printf ("Error al abrir file1.txt\n");
   }
   else {
      if (f2 == NULL) {
         printf ("Error al abrir file2.txt \n");
         fclose(f1);
      }
      else {
         //Bucle de copia carácter a carácter
         while((ch = fgetc(f1)) != EOF)
             fputc(ch,f2);

         fclose(f1);
         fclose(f2);

      }
   }
}
~~~

### Lectura y escritura de líneas completas: `fgets`y `fputs`

Estas funciones escriben / leen una cadena de caracteres en el archivo asociado.

La función `fputs`escribe una cadena de caracteres. Devuelve `EOF`si no ha podido escribir la cadena, y un valor no negativo si la escritura es correcta.

~~~c
int fputs (char *cadena, FILE *f)
~~~

La función `fgets` lee una cadena de caracteres del archivo. Termina cuando lee el fin de línea (línea completa) o bien cuando ha leído `tam-1`caracteres, siendo `tam`un número entero de la función. Devuelve un puntero a la cadena devuelta o `NULL`si ha habido error.

~~~c
char *fgets (char *cadena, int tam, FILE *f)
~~~
Le indicamos con `tam` cuántos caracteres leer. Si encuentra un `\n` solo devuelve lo leído hasta ese carácter (incluido). El valor leído se guarda en `cadena` y también se devuelve. Si se ha producido un error (fin de fichero, por ejemplo) se devuelve NULL.

Ejemplo: Lectura de un máximo de 80 caracteres:

~~~c
#define T 81 // contamos el '\0'

int main() {
   char cad[T];
   FILE *f;

   // instrucciones para abrir el fichero

   fgets(cad, T, f);
}
~~~

Ejemplo: Copiar ficheros línea a línea modo texto

~~~c
#define TAM 100

int main() {
   FILE *f;
   FILE *f2;
   char cad[TAM];

   f = fopen("ejemplo1.c","r");
   f2 = fopen("ejemplo3.c","w");

   if (f == NULL) {
      printf ("Error al abrir ejemplo1.c\n");
   }
   else {
      if (f2 == NULL) {
         printf ("Error al abrir ejemplo2.c \n");
         fclose(f);
      }
      else {
         while (!feof(f)) {
            if (fgets(cad, TAM, f) != NULL)
               fputs(cad, f2);
         }

         fclose(f);
         fclose(f2);
      }
   }
}
~~~


#### Lectura y escritura con formato: `fscanf`y `fprintf`

La función `fscanf`permite leer datos de un *stream*. Todos los formatos y opciones de `scanf`se pueden aplicar a `fscanf`.

~~~c
fscanf (FILE *f, char *formato...)
~~~

Ejemplo:

~~~c
int main(){
   FILE *f;
   int x;
   char c;
   char cad[15];

   f = fopen("ejemplo.txt", "r");
   if(f != NULL) {
      while (! feof(f)) {
         fscanf(f, "%d %c %s\n", &x, &c, cad);

         // aquí continuaría el código
      }
      fclose(f);
   }
}
~~~

Ejercicio: Crea un archivo de txt compatible con el ejemplo anterior y pruébalo.

Para escribir datos con formato en un *stream* se usa `fprintf`. Todos los formatos y opciones de `printf`se pueden aplicar a `fprintf`.

~~~c
fprintf (FILE *f, char * formato...)
~~~


Ejemplo:

~~~c
int main() {
   FILE *descriptor;

   // Creamos el archivo y lo abrimos para escritura

   descriptor = fopen("./ejemplo.txt", "w");
   if(descriptor == NULL)
      printf("Error, no se puede crear el archivo");
   else
      fprintf(descriptor, "%d", 1234);   // Escribimos algo

   //Cerramos el archivo
   fclose(descriptor);
}
~~~

Ejemplo: Queremos crear el archivo "datos.dat" de forma que cada línea contenga un registro con los datos de una persona: nombre, fecha nacimiento. Los campos de la estructura se escriben con `fprintf` en el fichero.

~~~c
typedef struct {
   char *nombre;
   int dia;
   int mes;
   int anyo;
}TPersona;

void entrada(TPersona *p);

int main() {
   FILE *f;
   char file[] = "datos.dat";
   char resp = 'S';
   TPersona p;

   p.nombre = NULL;

   if ((f = fopen(file, "w")) == NULL) {
      printf("Error al abrir el archivo\n");
   } else {
      while (toupper(resp) == 'S') {
         entrada(&p);
         fprintf(f, "%s %d-%d-%d\n",p.nombre, p.dia, p.mes, p.anyo);
         printf("Otro registro?: ");
         scanf("\n%c", &resp);
      }
      fclose(f);
      free(p.nombre);
      p.nombre = NULL;
   }
}

void entrada(TPersona *p) {
   char cad[25];
   printf("Nombre: ");
   scanf("%s", cad);
   p->nombre = (char*)realloc(p->nombre, (strlen(cad)+1)*sizeof(char));
   strcpy(p->nombre, cad);
   printf("Fecha nacimiento (dd mm aaaa): ");
   scanf("%d %d %d", &p->dia, &p->mes, &p->anyo);
}
~~~

### Funciones de entrada y salida para archivos binarios: `fread`y `fwrite`

Para abrir un archivo en modo binario hay que especificar la opción *b* en el modo de apertura. Los archivos binarios son secuencias de 0s y 1s, bloques de datos. Optimizan la memoria ocupada por un archivo, sobre todo con campos numéricos. Por ejemplo, para almacenar un entero, ocupa 2 *bytes*. Para leer un archivo binario se ha de realizar en modo binario y sólo se pueden visualizar desde el entorno de un programa C. Modos de apertura binario:

    "rb", "wb", "ab", "r+b", "w+b", "a+b"

Ejemplo: Abrir tres archivos en modo binario

~~~c
FILE *f1, *f2, *f3;
f1 = fopen("file1.ene", "rb");  // lectura binario
f2 = fopen("file2.feb", "w+b"); // leer/escribir binario
f3 = fopen("file3.mar", "ab");  // añadir a archivo binario
~~~

`fwrite`escribe un buffer de cualquier tipo de dato en un archivo binario. Permite escribir un número `num_el`de elementos, de tamaño `tam_el`, desde una zona de memoria indicada por `puntero`, a un *stream*.

~~~c
size_t fwrite (void *puntero, size_t tam_el, size_t num_el, FILE *stream)
~~~

Ejemplo: Guardamos en un archivo binario un conjunto de puntos:

~~~c
typedef struct {
   int x;
   int y;
}TPunto;

int main() {
   TPunto p;
   char *file = "puntos.dat";
   FILE *f;

   if ((f = fopen(file, "wb")) == NULL) {
      printf("Error en la apertura del fichero\n");
   }
   else {
      do {
         printf("Introduce las coordenadas del punto. Para acabar (0 0): ");
         scanf("%d %d", &p.x, &p.y);
         if (p.x != 0 && p.y != 0)
            fwrite(&p, sizeof(TPunto), 1, f);
      }while(p.x != 0 && p.y != 0);
      fclose(f);
   }
}
~~~

La función `fread`lee de un archivo n bloques de bytes y lo almacena en un buffer. El número de bytes de cada bloque (tamaño) se pasa como parámetro, al igual que el número n de bloques y la dirección del buffer o variable donde se almacena. La función devuelve el número de bloques que lee y debe coincidir con n.

~~~c
size_t fread (void *puntero, size_t tam, size_t n, FILE *f)
~~~

Ejemplo: Abrir archivo en modo binario para lectura. Leer el archivo hasta el final y cada lectura es un número real que se acumula en la variable `suma`:

~~~c
int main() {
   FILE *f;
   double x, suma = 0.0;

   if ((f = fopen("reales.num", "rb")) == NULL) {
      printf("Error al abrir el archivo\n");
   }
   else {
      while (!feof(f)) {
         fread(&x, sizeof(double), 1, f);
         suma += x;
      }
      fclose(f);
   }
}
~~~

Ejemplos de escritura de array de enteros en archivos binarios (la lectura es igual):

~~~c
int arr[3] = {10, 20, 30};
// Escribe el array entero:
fwrite(arr, sizeof(arr), 1, fp);
//Escribe los dos primeros elementos del array:
fwrite(arr, sizeof(int), 2, fp);
~~~

Ejemplos de escritura de array de `structs` en archivos binarios (usamos el `TPunto` definido previamente):

~~~c
TPunto puntos[3] = { {2,3},{3,5},{6,2} };
// Escribe el array entero:
fwrite(puntos, sizeof(puntos), 1, fp);
//Escribe los dos primeros elementos del array:
fwrite(puntos, sizeof(TPunto), 2, fp);
~~~

### Funciones de entrada y salida para tipos de datos compuestos

Si tenemos que escribir una estructura o registro en un *stream*, se puede hacer de dos formas:

- Escribir uno a uno cada uno de los campos, utilizando funciones como `printf`, etc.
- Escribir toda la estructura a la vez usando la función `fwrite`, indicando la dirección de comienzo y el tamaño del registro en bytes (obtenido con `sizeof`). Lo hemos vistro previamente con el ejemplo del punto.

La segunda estrategia es más eficiente. En el siguiente ejemplo vemos las dos formas:


~~~c
#define TAMCAD 15

typedef struct {
   char nombre[TAMCAD];
   char apellidos[TAMCAD];
   int edad;
}TPersona;

int main() {
   TPersona alumno;
   FILE *f, *f2;

   strcpy(alumno.nombre, "Pepe");
   strcpy(alumno.apellidos, "Garcia Sanchez");
   alumno.edad = 25;

   f = fopen("alumno.dat","wb");

   if (f == NULL) {
      printf ("Error al abrir fichero\n");
   }
   else {
      // Escribimos el registro de una sola vez
      fwrite(&alumno,         // dirección de comienzo
             sizeof(alumno),  // tamaño
             1,               // número de elementos
             f);              // descriptor del fichero

      fclose(f);
   }

   f2 = fopen("alumno.txt","w");

   if (f2 == NULL) {
      printf ("Error al abrir fichero\n");
   }
   else {

      // Escribimos a continuación el registro campo a campo
      fprintf(f2, "\n%s\n", alumno.nombre);
      fprintf(f2, "%s\n", alumno.apellidos);
      fprintf(f2, "%d", alumno.edad);

      fclose(f2);
   }
}
~~~


Ejemplo pasando el nombre del fichero como parámetro a `main`:

~~~c
#define TAM 2048

// Ejemplo de lectura y escritura binaria, pasamos el nombre del fichero como parámetro a main

int main(int argc, char **argv) {
   FILE *fe, *fs;
   char buffer[TAM];
   int bytesLeidos;

   // Abrir el fichero de entrada en lectura y binario
   fe = fopen(argv[1], "r");

   if(!fe) {
      printf("El fichero %s no existe o no puede ser abierto.\n", argv[1]);
   } else {
      // Crear o sobreescribir el fichero de salida en binario
      fs = fopen(argv[2], "wb");

      if(!fs) {
         printf("El fichero %s no puede ser creado.\n", argv[2]);
         fclose(fe);
      }else {
      // Bucle de copia:
         while((bytesLeidos = fread(buffer, 1, TAM, fe)))
            fwrite(buffer, 1, bytesLeidos, fs);
         // Cerrar ficheros:
         fclose(fe);
         fclose(fs);
      }
   }
}
~~~


### Ejercicios resueltos

1. Hacer un programa que pida palabras al usuario y que las guarde en un fichero. El programa finalizará cuando el usuario introduzca "fin".2. Hacer un programa que pregunte el nombre de un fichero. Si existe, deberá mostrar el contenido del fichero de 25 en 25 líneas. Cuando muestre 25 líneas, esperará hasta que el usuario pulse una tecla (`getchar`) y mostrará las siguientes 25 líneas.
3. Crear un programa que pida al usuario pares de números enteros y escriba su suma (con el formato `20 + 3 = 23`) en pantalla y en un fichero llamado "sumas.txt". Cada vez que se ejecute el programa, deberá añadir los nuevos resultados a continuación de los resultados de las ejecuciones anteriores.


#### Solución ejercicio 1
~~~c
#define TAMCAD 60

int main() {
   FILE* pf;
   char fin[]="fin";
   char palabra[TAMCAD];

   pf = fopen("palabras.txt", "w");

   if (pf == NULL) {
      printf ("Error al abrir fichero\n");
   }
   else {
      do {
          printf("\nEscriba una palabra (fin para terminar). \n");
          scanf("%s",palabra);

          if (strcmp(palabra, fin) != 0)
            fprintf(pf, "%s\n", palabra);

       } while (strcmp(palabra, fin) != 0);

      fclose(pf);
   }
}

~~~

#### Solución ejercicio 2

~~~c
#define TAMLINEA 100
#define TAM 20

int main() {
   FILE* f;
   char linea[TAMLINEA], nombre[TAM];
   int i;

   printf("\nIntroduzca el nombre de fichero: ");
   scanf("%s",nombre);

   f = fopen(nombre, "r");

   if (f != NULL) {
      while (!feof(f))  {
        for (i = 0; i < 25; i++) {
            fgets(linea, TAMLINEA, f);
            if (!feof(f)) {
                printf("%s\n",linea);
            }
         }
         getchar();
      }
      fclose(f);
   }
}

~~~

#### Solución ejercicio 3

~~~c
int main()
{
   FILE *resultados;
   int numero1=0, numero2=0, suma=0;

   if((resultados = fopen("sumas.txt", "a+")) == NULL)
      printf("No se pudo abrir el archivo.\n");
   else
   {
      printf("Escriba dos numeros.\n\"000\" para salir.\n");
      do
      {
         printf("Primer numero: ");
         scanf("%d", &numero1);
         if (numero1 != 0) {
            printf("Segundo numero: ");
            scanf("%d", &numero2);
            suma = numero1 + numero2;
            printf("%d + %d = %d\n", numero1, numero2, suma);
            fprintf(resultados, "%d + %d = %d\n", numero1, numero2, suma);
         }
      }
      while (numero1 != 0);
      fclose(resultados);
   }
}
~~~

## Ejercicios propuestos

1. Escribe un programa que lea de un fichero de texto los elementos de una matriz cuadrada y muestre un mensaje en pantalla indicando si es o no simétrica.

    Recuerda que una matriz cuadrada de dimensión N es simétrica si aij = aji para todo i,j con i, j = 1,2,3,4,...,N.

    El nombre del fichero se pasará como parámetro al programa a través de la línea de comandos. Si el fichero no se puede abrir o no se indica ninguno, el programa deberá terminar su ejecución.

    El fichero de texto tendrá el siguiente formato, que suponemos que siempre será correcto:
En la primera línea se indica la dimensión de la matriz cuadrada.
Las siguientes líneas contendrán los elementos de cada fila de la matriz (una fila por cada línea).

    Ten en cuenta además que tu programa deberá reservar **sólo la memoria necesaria** para guardar los elementos de la matriz.

    Ejemplos de ficheros:

    ~~~text
fichero1.txt:
3
1 2 3
2 4 5
3 5 6
~~~

    ~~~text
fichero2.txt:
4
1  2   3  4
5  6   7  8
9  10 11 12
13 14 15 16
    ~~~

    Ejemplos de ejecución:

    ~~~text
$ ./miPrograma fichero1.txt
La matriz almacenada en el fichero fichero1.txt ES SIMETRICA
$ ./miPrograma fichero2.txt
La matriz almacenada en el fichero fichero2.txt NO ES SIMETRICA
$ ./miPrograma
Falta argumento en la línea de comandos o el fichero no se puede leer
    ~~~

2. Dada la definición del siguiente tipo de dato:

    ~~~c
typedef struct {
   int a;
   float b;
   char c;
}TElem;
    ~~~

    a. Añade un nuevo tipo de dato llamado `TElementos` que contenga un vector dinámico cuyos elementos son de tipo `TElem y un número que indique el total de elementos que contiene el vector.

    b.  Define la función `leerYRellenar` que recibe como parámetros un nombre de fichero de texto y el tipo `TElementos` definido previamente. La función debe leer el contenido del fichero y almacenarlo en el vector, que irá creciendo dinámicamente conforme se lean líneas del fichero. El formato de cada línea del fichero es [int float char], ejemplo:

    ~~~text
3 1.5 A
4 8.9 B
1 5.2 C
    ~~~

    c.  Completa el `main()` para:
realizar la llamada a la función anterior  
imprimir por pantalla el contenido del vector.
liberar la memoria reservada dinámicamente

~~~c
int main() {
   TElementos elems;
   char nombre[] = "fichero.txt";

   leerYRellenar(nombre, &elems);  // rellena aquí la llamada

  // Escribe aquí tu código para imprimir el contenido del vector:



  // Escribe a continuación el código para liberar la memoria reservada:
~~~
---

Programación 1, Grado de Robótica, curso 2020-21  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Cristina Pomares Puig
