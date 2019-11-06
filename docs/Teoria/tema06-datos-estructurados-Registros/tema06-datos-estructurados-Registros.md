
# Tema 6: Tipos de datos estructurados: Registros

## 1. Registros

Los tipos de datos compuestos o estructurados, son tipos compuestos por otros tipos. Vimos que habían dos tipos:

- Array: Está compuesto por elementos del mismo tipo. Por ejemplo, un array de enteros, todos sus elementos son enteros.
- Registro o estructura: Está compuesto por elementos heterogéneos, pueden tener distintos tipos.

#### Definición

Un registro es un tipo de datos que permite agrupar bajo un mismo nombre elementos del mismo o de distinto tipo de datos, que se encuentran relacionados entre sí.

Cada elemento se denomina **campo** o **miembro** de la estructura. Un registro permite encapsular entidades donde cada campo representa los atributos o propiedades de dicha entidad.

Caraterísticas:

- Un registro o estructura es la manera que tenemos de encapsular variables de diferentes tipos bajo una única entidad: nos referimos a ellos con un identificador único.
- Tienen la peculiaridad de que las variables que forman parte del registro estarán alineadas en memoria: eficiencia
- En un registro se agrupan atributos de una entidad
- Cada uno de los elementos de un registro se denomina **campo**. Para referirse a un determinado elemento de un registro se deberá utilizar el identificador del registro, seguido de un punto ‘.’ y del identificador del campo correspondiente

> Persona:
>
> 	- Nombre
> 	- Apellidos
> 	- NIF
> 	- edad
> 	- género
>
> Dirección:
>
> 	- Calle
> 	- Número
> 	- CP
> 	- Población
> 	- Provincia
>
> Cliente:
>
> 	- NumCliente
> 	- Persona
> 	- Dirección
> 	- Empresa
>

Diferencias respecto a los arrays:

- Los elementos de un array son todos del mismo tipo, en una estructura no.
- En un array se selecciona un elemento por su posición dentro del array, en una estructura cada elemento tiene su identificador

### 1.1 Definición de un registro

La sintaxis es:

~~~text
struct nombreRegistro {
   tipo-campo1 nombre-campo1
   tipo-campo2 nombre-campo2
   ...
};
~~~

Pueden utilizarse arrays como campos. Ejemplo:

~~~c
struct CD {
   char titulo[20];
   char artista[25];
   int num_canciones;
   float precio;
};
~~~

Sintaxis utilizando `typedef`:

~~~text
typedef struct {...} nombreRegistro;
~~~

Dentro de las llaves escribiremos los campos que va a contener el registro.

~~~c
typedef struct {
   char nombre[20];
   char apellidos[30];
   char nif[10];
   int edad;
   char genero;
} TPersona;

int main() {
   // Declaración de variables de estructuras
   struct CD cd1;
   struct CD cd2;

   // Declaración de variables de estructuras definidas con typedef
   TPersona persona1;

   return 0;
}
~~~

#### Uso de los registros

Con un registro se puede trabajar a dos niveles: con el registro completo y con sus campos.

Podemos utilizar la operación de asignación entre registros, pero no la de comparación. Es decir, podemos asignar a una variable de tipo `struct` el valor de otra del mismo tipo. También es posible pasar un registro como parámetro a una función y que una función devuelva un registro.

En el siguiente ejemplo, asignamos una estructura a otra:

~~~c
cd1 = cd2;
~~~

#### Inicialización de registros

Podemos inicializar los registros al definir las variables o dejarlos vacíos para manejarlos más adelante:

~~~c
   struct CD cd1 = {
      "Wish",      // album
      "The Cure",  // artista
      7,           // num_canciones
      21.5         // precio
   };

   TPersona persona1 = {   // definido con typedef
      "Pepe",
      "García",
      "32112234z",
      55,
      'V'
   };
~~~

### 1.2 Operadores para manejo de registros

#### El operador `.`
Para acceder a los campos de una variable de tipo registro utilizamos el operador punto `.`. Este operador proporciona el camino directo al campo correspondiente. Los datos deben ser del mismo tipo que el tipo declarado para ese campo.

~~~c
TPersona persona2;

strcpy(persona2.nombre, "María");
strcpy(persona2.apellidos, "Sánchez");
strcpy(persona2.nif, "11222433A");
persona2.edad = 25;
persona2.genero = 'M';
~~~


#### El operador `->`

Para acceder a los campos de una variable de tipo puntero (lo veremos en el siguiente tema) a registro utilizamos el operador puntero `->`. Este operador indica que en la parte izquierda está la dirección de memoria de un registro, y la parte derecha los campos del mismo.

~~~text
<puntero_estructura> -> <nombre_campo> = datos;
~~~

Es el caso, por ejemplo, de los registros pasados como parámetro por referencia a una función. La función recibe como argumento la dirección de memoria (puntero) del registro.

~~~c
void rellena (TPersona *p) {
    strcpy(p->nombre, "Pepe");
    strcpy(p->apellidos, "Garcia");
    p->edad = 45;
}
~~~

### 1.3  Registros y funciones

#### Paso de registros como parámetros a funciones

- De forma general:	- Paso por valor cuando se use la información delregistro sin modificarlo	- Paso por referencia cuando modifiquemos algún campo del registro, pasando la dirección de memoria utilizando el operador `&`.

- De forma excepcional, tendremos en cuenta que en algunos casos el tamaño del registro en memoria puede ser elevado, por lo que valoraremos en la implementación cuándo nos conviene pasarlo por valor o por referencia, independientemente de si se modifican o no sus campos.  


#### Funciones que devuelven registros

Vamos a seguir la misma norma que cuando tratamos tipos de datos simples, es decir, cuando sólo se va a devolver un dato (en este caso un registro), se hará a través de `return`.

~~~c
typedef struct {
   int x;
   int y;
}TPunto;

// prototipos de funciones
TPunto leerPunto();
void imprimePunto(TPunto);
void swap(TPunto*, TPunto*);

int main() {
   TPunto p1, p2;

   p1 = leerPunto();
   p2 = leerPunto();

   imprimePunto(p1);
   imprimePunto(p2);

   swap(&p1, &p2);

   imprimePunto(p1);
   imprimePunto(p2);

   return 0;
}

TPunto leerPunto() {
    TPunto p;
    printf("Coordenada x del punto:");
    scanf("%d",&p.x);
    printf("Coordenada y del punto:");
    scanf("%d",&p.y);
    return p;
}

void imprimePunto(TPunto punto) {
    printf("[X:%d, Y:%d]\n", punto.x, punto.y);
}

void swap(TPunto* p1, TPunto* p2) {
   TPunto aux;

   aux.x = p1->x;
   aux.y = p1->y;
   p1->x = p2->x;
   p1->y = p2->y;
   p2->x = aux.x;
   p2->y = aux.y;
}

~~~

### 1.4 Estructuras anidadas

Un registro puede contener otros registros. Ejemplo:

~~~c
typedef struct {
   char nombre[20];
   char apellidos[30];
   char nif[10];
   int edad;
   char genero;
} TPersona;

typedef struct{
   int codCliente;
   TPersona datosCliente;
   char direccion[100];
   char nombreEmpresa[50];
} TCliente;

int main(){
   TCliente cli;

   cli.codCliente = 4;
   strcpy(cli.direccion, "Avda Mediterraneo 45");
   cli.datosCliente.edad = 30;
   strcpy(cli.datosCliente.nombre, "Juan");

   return 0;
} 
~~~

### 1.5 Arrays de registros

Podemos definir arrays donde su tipo base sea un registro, es decir, cada elemento del vector es un registro, con memoria reservada para su uso. Ya que en los arrays sólo podemos almacenar diversos valores de un mismo tipo, los arrays de estructuras permiten almacenar diversos valores de diferentes tipos agrupados en registros.

~~~c
typedef struct {
   char nombre[50];
   float precio;
   int stock;
} TProducto;

TProducto vectorProductos[100];
~~~

Para acceder a los campos de cada uno de los elementos, se recorre el array y se accede a cada elemento como lo hacemos con otros tipos de dato:

~~~c
strcpy(vectorProductos[0].nombre, "Libro Programación en C");
vectorProductos[0].precio = 17.5
vectorProductos[0].stock = 4;
~~~

## 2. Uniones

Las uniones son similares a las estructuras en cuanto que agrupan una serie de datos, pero la forma de almacenamiento es diferente:

- Las estructuras almacenan variables relacionadas juntas y almacenadas en posiciones contiguas de memoria.
- Las uniones almacenan también múltiples campos, pero todos ellos se solapan entre sí en la misma posición. Para determinar el tamaño de una unión se analiza el tamaño de cada campo y el de mayor tamaño será el tamaño de la unión.

Una razón para usarlas es ahorrar memoria. Se usan cuando se tienen varios variables relacionadas de alguna forma, pero no se van a usar al mismo tiempo. Por ejemplo, si tenemos una estructura para almacenar una imagen de 256x256 píxeles, y cada imagen las tenemos codificada en un formato, podemos utilizar una misma estructura para almacenar una imagen, que puede estar en formatos diferentes y sólo ocuparía el mayor tamaño.

Sintaxis:

~~~text
union nombre-union {
    tipo1 campo1;
    tipo2 campo2;
    ...
};
~~~

La forma de acceder a los campos de una unión es igual que en las estructuras.

También se pueden definir con `typedef`.


Ejemplo:

~~~c
union ejemplo {
    char letra;
    double altura;
};

// Definido con typedef:
typedef union {
    char letra;
    double altura;
}TEjemplo;
~~~

La cantidad total de memoria utilizada por la union es de 8 bytes, ya que el campo `double altura`es el mayor.

Ejemplo:

~~~c
typedef union {
   int a;
   char b;
}TPrueba;

int main() {
   TPrueba p1;
   p1.a = 50;
   p1.b = 'A';
   printf("p1.a: %d p1.b: %c\n", p1.a, p1.b);

   return 0;
}

// Salida:
// p1.a: 65 p1.b: A
~~~

Las uniones también nos sirven para **generalizar**. En el siguiente ejemplo, tenemos una estructura para almacenar DVD y otra para almacenar CD. Queremos hacer un array genérico que almacene dispositivos tanto de DVD como de CD. Para ello creamos otra estructura TDispositivo genérica, que almacenará o un CD o un DVD. El array lo definimos de tipo TDispositivo, por lo que podrá almacenar en cada posición un CD o un DVD.

~~~c
#define TAM 2

typedef enum {CD, DVD} TTipoDisp;

typedef struct{
   char titulo[20];
   char artista[25];
   int num_canciones;
   float precio;
} TCD;

typedef struct{
   char titulo[20];
   char director[25];
   float precio;
} TDVD;

typedef struct {
   TTipoDisp tipo;
   union{
      TCD cd;
      TDVD dvd;
   }disp;
}TDispositivo;

void imprimeDisp(TDispositivo []);

int main() {
   TDispositivo disp[TAM];
   TCD cd1 = {
      "Hopes and fears",
      "Keane",
      7,
      17.99
   };
   TDVD dvd1 = {
      "Spiderman",
      "Sam Raimi",
      9.99
   };

   disp[0].disp.cd = cd1;
   disp[0].tipo = CD;

   disp[1].disp.dvd = dvd1;
   disp[1].tipo = DVD;

   imprimeDisp(disp);

   return 0;
}

void imprimeDisp(TDispositivo arrayDisp[]) {
   int i;

   for(i = 0; i < TAM; i++) {
      printf("Tipo: %d\n",arrayDisp[i].tipo);
      switch(arrayDisp[i].tipo) {
         printf("Tipo: %d\n",arrayDisp[i].tipo);
         case CD:
            printf("***************\n");
            printf("Título: %s\n", arrayDisp[i].disp.cd.titulo);
            printf("Artista: %s\n", arrayDisp[i].disp.cd.artista);
            break;
         case DVD:
            printf("***************\n");
            printf("Título: %s\n", arrayDisp[i].disp.dvd.titulo);
            printf("Director: %s\n", arrayDisp[i].disp.dvd.director);
            break;
      }
   }
}
~~~

---

### Ejercicio 1

Define los tipos de datos necesarios que permitan almacenar los datos de 100 alumnos. De cada alumno se quiere almacenar su nombre, apellidos y dirección. Cada uno tiene 10 asignaturas compuestas de código de la asignatura y nota.

~~~c
//En primer lugar definimos las constantes necesarias.

#define TAMCAD 45
#define TAMASIG 3
#define NUMASIG 10
#define NUMALU 100

//Definimos las estructuras necesarias
//Cada alumno tiene 10 asignaturas compuesto de código de la asignatura y nota
typedef struct {
   char codigoAsignatura[TAMASIG];
   float nota;
}TAsignatura;

//Estructura con la información de los alumnos
typedef struct {
   char nombre[TAMCAD];
   char apellidos[TAMCAD];
   char direccion[TAMCAD];
   TAsignatura asig[NUMASIG];
}TFichaAlumno;

//Array que contendrá los datos de todos los alumnos
typedef TFichaAlumno TAlumnos [NUMALU];
~~~

### Ejercicio 2

Escribe un programa que guarde información de 30 alumnos. De cada alumno leeremos su número de expediente, nombre, fecha de nacimiento, fecha de ingreso y su nota media. El programa debe permitir dar de alta un alumno y mostrar todos los alumnos.

~~~c
#define TAMCAD 45
#define NUMALU 30

typedef struct {
   int dia;
   int mes;
   int anyo;
}TFecha;

typedef struct {
   int exp;
   char nombre[TAMCAD];
   TFecha fechaNac;
   TFecha fechaIng;
   float notaMedia;
}TFichaAlumno;

//Array de alumnos
typedef TFichaAlumno TAlumnos[NUMALU];

//Prototipos funciones
void mostrarFecha(TFecha);
void mostrarAlumnos(TAlumnos, int);
void darDeAltaAlumno(TAlumnos, int *);
void pedirFecha(TFecha *);
int pedirOpcion();

int main(){
   TAlumnos alumnos;
   int opcion, numAlumnos;
   numAlumnos = 0;

   do{
      opcion = pedirOpcion();

      switch(opcion){
         case 1:
            if(numAlumnos < NUMALU)
               darDeAltaAlumno(alumnos, &numAlumnos);
            else
               printf("No es posible introducir más alumnos");
            break;
         case 2:
            mostrarAlumnos(alumnos, numAlumnos);
            break;
         case 3:
            printf("Terminado\n");
            break;
         default:
            printf("Opción incorrecta\n");
      }
   }while(opcion != 3);

   return 0;
}

int pedirOpcion() {
   int opcion;

   printf("******Gestión de alumnos******\n");
   printf("Opciones disponibles: \n");
   printf("1. Dar de alta un alumno\n");
   printf("2. Mostrar listado alumnos\n");
   printf("3. Salir\n");
   printf("Seleccione una opción: ");
   scanf("%d", &opcion);

   return opcion;
}

//Muestra la fecha separada por /
void mostrarFecha(TFecha fecha){
   printf("%d / %d / %d\n",fecha.dia, fecha.mes,fecha.anyo);
}

void mostrarAlumnos(TAlumnos alumnos, int numAlumnos) {
   int i;

   for(i = 0; i<numAlumnos;i++) {
      printf("Alumno: %d\n", alumnos[i].exp);
      printf("Nombre: %s\n", alumnos[i].nombre);
      printf("Fecha de nacimiento: ");
      mostrarFecha(alumnos[i].fechaNac);
      printf("Fecha de ingreso: ");
      mostrarFecha(alumnos[i].fechaIng);
      printf("Nota media: %.2f\n", alumnos[i].notaMedia);
   }
}

//Solicita la fecha
void pedirFecha(TFecha *fecha) {
   printf("\tIntroduce día:");
   scanf("%d", &fecha->dia);
   printf("\tIntroduce mes: ");
   scanf("%d", &fecha->mes);
   printf("\tIntroduce año: ");
   scanf("%d", &fecha->anyo);
}

//Solicita los datos de los alumnos
void darDeAltaAlumno(TAlumnos alumnos, int *numAlumnos) {
   int i;

   i = *numAlumnos;
   printf("Introduce el número de expediente: ");
   scanf("%d", &alumnos[i].exp);
   printf("Introduce el nombre: ");
   scanf("%s",alumnos[i].nombre);
   printf("Fecha de nacimiento:\n");
   pedirFecha(&alumnos[i].fechaNac);
   printf("Fecha de ingreso:\n");
   pedirFecha(&alumnos[i].fechaIng);
   printf("Introduce la nota media: ");
   scanf("%f", &alumnos[i].notaMedia);
   (*numAlumnos)++;
}
~~~

### Ejercicio 3

Escribe los tipos de datos adecuados para almacenar triángulos. De cada triángulo se quiere guardar los tres puntos de sus vértices, su área y su perímetro.
Se pide leer un triángulo por teclado: únicamente se leerán sus tres puntos. Su área y su perímetro se calcularán automáticamente después de la lectura.

~~~c
#include <stdio.h>
#include <math.h>

typedef struct {
   int x;
   int y;
}TPunto;

typedef struct {
   TPunto p1;
   TPunto p2;
   TPunto p3;
   float area;
   float perimetro;
}TTriangulo;

TTriangulo leerTriangulo();
void calculaLados(TTriangulo, float *, float *, float *);
void calculaPerimetroYArea(TTriangulo *);

int main() {
   TTriangulo triangulo;

   triangulo = leerTriangulo();

   printf("El perímetro del triángulo es: %.2f\n",triangulo.perimetro);
   printf("El área del triángulo es: %.2f\n",triangulo.area);

   return 0;
}

TTriangulo leerTriangulo() {
   TTriangulo triangulo;

   printf("Introduzca las coordenadas del punto 1:\n");
   scanf("%d %d",&triangulo.p1.x,&triangulo.p1.y);
   printf("Introduzca las coordenadas del punto 2:\n");
   scanf("%d %d",&triangulo.p2.x,&triangulo.p2.y);
   printf("Introduzca las coordenadas del punto 3:\n");
   scanf("%d %d",&triangulo.p3.x,&triangulo.p3.y);

   calculaPerimetroYArea(&triangulo);

   return triangulo;
}

void calculaPerimetroYArea(TTriangulo *triangulo) {
   float s, lado1, lado2, lado3;

   calculaLados(*triangulo, &lado1, &lado2, &lado3);

   triangulo->perimetro = lado1 + lado2 + lado3;

   // Fórmula de Herón
   s = 1.0/2.0 * triangulo->perimetro;
   triangulo->area = sqrt(s *
                         (s - lado1) *
                         (s - lado2) *
                         (s - lado3));
}

void calculaLados(TTriangulo triangulo, float *lado1, float *lado2, float *lado3) {
   *lado1 = sqrt(pow(triangulo.p1.x - triangulo.p2.x, 2) +
                 pow(triangulo.p1.y - triangulo.p2.y, 2));
   *lado2 = sqrt(pow(triangulo.p1.x - triangulo.p3.x, 2) +
                 pow(triangulo.p1.y - triangulo.p3.y, 2));
   *lado3 = sqrt(pow(triangulo.p3.x - triangulo.p2.x, 2) +
                 pow(triangulo.p3.y - triangulo.p2.y, 2));
}
~~~

## Ejercicios propuestos

### Ejercicio 4

Vamos a partir del ejercicio de los triángulos. Queremos almacenar 10 triángulos y ordenarlos de menor a mayor perímetro. Muéstralos ordenados por pantalla, puedes usar el algoritmo de ordenación que prefieras. Puedes hacer una función que imprima los datos de un triángulo por pantalla.

### Ejercicio 5

Define un nuevo tipo `TRectangulo` y añade la misma funcionalidad que para los triángulos: área y perímetro.

### Ejercicio 6

Dada la siguiente definición de tipos de datos:

~~~c
typedef enum {TRIANGULO, RECTANGULO} TTipoFigura;

typedef struct {
   int x;
   int y;
}TPunto;

typedef struct {
   TPunto p1;
   TPunto p2;
   TPunto p3;
   float area;
   float perimetro;
}TTriangulo;

typedef struct {
   TPunto p1;  //esquina inferior izquierda
   TPunto p2;  //esquina superior derecha
   float area;
   float perimetro;
}TRectangulo;

typedef struct {
   TTipoFigura tipo;
   union{
      TTriangulo triangulo;
      TRectangulo rectangulo;
   }fig;
}TFigura;
~~~

Define un array genérico de figuras de tipo `TFigura`. Podrá contener tanto triángulos como rectángulos. Implementa una función que reciba dicho array e imprima los datos de la figura que contiene en cada posición.

----
Programación 1, Grado de Robótica, curso 2019-20  
© Departamento Ciencia de la Computación e Inteligencia Artificial, Universidad de Alicante  
Cristina Pomares Puig
