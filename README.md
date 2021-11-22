<img  align="left" width="150" style="float: left;" src="https://www.upm.es/sfs/Rectorado/Gabinete%20del%20Rector/Logos/UPM/CEI/LOGOTIPO%20leyenda%20color%20JPG%20p.png">

<br/><br/>

# Práctica 3 - Habilidades


## Contenido

-   [Requisitos previos](#requisitos-previos)
-   [Temas relacionados con la práctica](#temas-relacionados-con-la-practica)
-   [Convenciones](#convenciones)
-   [Objetivos](#objetivos)
-   [Introducción](#introducción)
-   [Actividades de la práctica](#actividades-de-la-práctica)
    -   [1. Lista de la compra](#1.-lista-de-la-compra)
    -   [2. Ordenación de la lista de la compra](#2.-ordenación-de-la-lista-de-la-compra)
    -   [3. Menú de selección](#3.-menú-de-selección)
-   [Evaluación](#evaluación)
-   [Entrega de la práctica](#entrega-de-la-práctica)

## Requisitos previos

Disponer de una versión de Python igual o superior a 3.10, y del entorno de desarrollo Visual Studio Code.

## Temas relacionados con la práctica

En la realización de este proyecto se ponen en práctica conceptos abordados entre los temas 1 y 7 de la asignatura.

## Convenciones

Durante la práctica se utilizarán tres tipos de código. Por un lado, código a escribir en la línea de comandos
(_command line_), también conocida como terminal o consola. En el ejemplo de abajo, vemos cómo ejecutamos
el comando ```python --version```, que imprime por pantalla la versión de Python en el sistema.

```shell
$ python --version
Python 3.8.10
```

Por otro lado, hay fragmentos de sesión del intérprete de comandos de python.
Podemos acceder al intérprete directamente ejecutando el comando Python en nuestra terminal:

```shell
$ python
Python 3.8.10 (default, Jun  2 2021, 10:49:15) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

En este punto, podemos empezar a introducir nuestro código Python.
Las líneas introducidas por el usuario son las que empiezan con "```>>>```" o "```...```", como en el ejemplo siguiente:

```python
Esto es código python
>>> a = 2
>>> for i in range(a):
...     print(i)
...
0
1
```

Finalmente, habrá código de ejemplo a guardar en un fichero de texto:

```python
def funcion(parametro):
   return
```

También utilizaremos notas para resaltar consejos o aspectos importantes:

_**Nota**: todas las líneas ejecutadas durante una sesión de python o de consola se guardan en el historial. Se puede acceder a una línea anterior mediante las flechas del teclado o pulsando ```Ctrl+P``` repetidamente hasta llegar a la línea deseada._

## Objetivos

-   Uso interactivo del intérprete de Python (REPL)
-   Uso básico de un IDE (Visual Studio Code) para desarrollar y ejecutar código
-   Uso de clases para encapsular estado y comportamiento
-   Refactorización de un paradigma orientado a funciones a uno orientado a objetos
-   Comprender conceptos básicos de ingenierı́a de software como interfaces

## Introducción

En prácticas anteriores se han desarrollado varias funciones independientes para cumplir diferentes cometidos: conversión de criptomonedas, lista de la compra, etc. También hemos visto cómo desarrollar menús interactivos que ofrecı́an esas funcionalidades al usuario.

En esta práctica el objetivo es conseguir que cualquier desarrollador pueda programar sus propias funcionalidades, compartirlas con el resto, e introducir funcionalidades desarrolladas por otros usuarios de manera sencilla. Nos inspiraremos directamente en el ejemplo de asistentes personales (p.e., alexa o Mycroft), que permiten añadir nuevas funcionalidades personalizadas.

Nuestra solución de prácticas anteriores tiene dos puntos débiles para conseguir este objetivo. Primero de todo, nos encontramos que algunas funciones están muy relacionadas (p.e., convertir a euros y convertir a bitcoins, o las diferentes funciones relacionadas con la lista de la compra), pero no existe una relación explı́cita en el código. Es decir, para saber qué funciones están relacionadas hay que leer con detenimiento el código. Además de dificultar el entendimiento del código, eso nos puede llevar a código desactualizado y a errores. Por otro lado, para crear los
menús de usuario vemos que hay que introducir manualmente las funciones, ya sea usando sentencias de control (proyecto 1) o un diccionario de comandos a funciones (proyecto 2).

Para solucionar estos problemas, haremos dos cosas. Lo primero que haremos es introducir el concepto genérico de habilidad. Ası́, nos encontrarı́amos la habilidad de convertir criptomonedas, la de gestionar la lista de la compra, etc. Cada una de estas habilidades puede encapsular internamente una o más funciones de las que ya desarrollamos en prácticas anteriores. Después, modificaremos nuestro menú para lidiar con habilidades en lugar de funciones.

El primer paso para desarrollar la práctica es descargar los ficheros necesarios del repositorio de Github. El método más sencillo es a través del botón ```Code->Download ZIP```. Los dos ficheros necesarios para la práctica son ```habilidades.py``` y ```test.py```.
El primero es un fichero de plantilla que contiene la definición de varias funciones que son útiles para la práctica (este será el fichero que se debe entregar en Moodle). Para su edición, se puede usar cualquier IDE, aunque se recomienda Visual Studio Code. Para comprobar las soluciones, se proponen dos opciones. Por otro lado, el fichero ```test.py```, se puede usar opcionalmente para comprobar que las funciones desarrolladas en la práctica funcionan correctamente, como veremos más adelante.

## Actividades de la práctica

### 1. Clase habilidad básica

Vamos a empezar por crear una clase simple para las habilidades. Por ahora, sólo consideraremos que las habilidades son una entidad (algo) que se puede invocar, y que nos proporcionan algún tipo de ayuda sobre su funcionamiento:

```python
class Habilidad:
  
  def invocar(self) -> void:
    print('Se ha invocado una habilidad que no hace nada')
  
  def ayuda(self) -> void:
    print('No hay ayuda especı́fica')
```
En este punto, podemos crear varias habilidades, pero no sirve para mucho porque todas las instancias hacen exactamente lo mismo. El resultado es igual que tener una función, pero con engorrosos pasos adicionales:

```python
>>> habilidad1 = Habilidad()
>>> habilidad2 = Habilidad()
>>> habilidad1.invocar()
Se ha invocado una habilidad que no hace nada
>>> habilidad2.invocar()
Se ha invocado una habilidad que no hace nada
```

Hagamos las habilidades algo más interesantes añadiéndoles algo de estado. El estado es un conjunto de valores internos en cada instancia de la clase. En nuestro caso, añadiremos un nombre para la habilidad y un pequeño texto de descripción de la habilidad. El nombre nos permitirá diferenciar entre habilidades de la misma clase en nuestro menú, y la descripción será útil para el usuario cuando implementemos un menú.

Si no se proporciona una descripción al crear una instancia, se reutilizará por defecto la documentación de la clase en cuestión. Esto es muy parecido a lo que hicimos en prácticas anteriores. Por último, también modificaremos ligeramente la función de ayuda para que intente reutilizar la documentación de la función invocar. El resultado es este:

```python
class Habilidad:
  '''Abstracción del concepto de habilidad en un asistente.'''

  def __init__(self, nombre, descripcion=None):
    self.nombre = nombre
    self.descripcion = descripcion or self.__doc__

  def invocar(self):
    print(f'Se ha invocado la habilidad {self.nombre}')

  def ayuda(self):
    texto = (self.invocar.__doc__) or 'No hay ayuda especı́fica'
    print(texto)
```

Con esta nueva clase podemos crear instancias diferentes, que no se comportan del todo igual, porque su estado interno es diferente. Por ejemplo:

```
>>> habilidad1 = Habilidad(1)
>>> habilidad2 = Habilidad(2)
>>> habilidad1.invocar()
Se ha invocado la habilidad 1
>>> habilidad2.invocar()
Se ha invocado la habilidad 2
>>> habilidad2.nombre
2
>>> habilidad2.descripcion
'Abstracción del concepto de habilidad en un asistente.'
>>> habilidad3 = Habilidad(3, descripcion='descripcion personalizada')
>>> habilidad3.descripcion
'descripcion personalizada'
```