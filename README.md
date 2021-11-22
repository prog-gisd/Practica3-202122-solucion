<img  align="left" width="150" style="float: left;" src="https://www.upm.es/sfs/Rectorado/Gabinete%20del%20Rector/Logos/UPM/CEI/LOGOTIPO%20leyenda%20color%20JPG%20p.png">

<br/><br/>

# Práctica 2 - Lista de la compra


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

Disponer de una versión de Python igual o superior a 3.8, y del entorno de desarrollo Visual Studio Code.

## Temas relacionados con la práctica

En la realización de este proyecto se ponen en práctica conceptos de los temas 1, 2, 3, 4, 5 y 6 de la asignatura. Además, se
utilizarán tangencialmente algunos elementos de temas posteriores.

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
-   Creación, modificación y recorrido de listas
-   Uso de diccionarios
-   Uso de funciones con argumentos opcionales

## Introducción

El objetivo de esta práctica es desarrollar un gestor de la lista de la compra que nos permita tener una lista de productos que queremos comprar.

En la primera práctica se desarrolló una versión inicial muy simple de este gestor. Esta práctica consistirá en la ampliación del gestor de la lista de la compra con varias funciones.

El primer paso para desarrollar la práctica es descargar los ficheros necesarios del repositorio de Github. El método más sencillo es a través del botón ```Code->Download ZIP```. Los dos ficheros necesarios para la práctica son ```listadelacompra.py``` y ```test.py```.
Las funciones desarrolladas deben estar contenidas en el fichero python con el nombre ```listadelacompra.py``` (que será el fichero que se debe entregar en Moodle). Este fichero se puede descargar del repositorio Github de la práctica, y contiene la cabecera de las funciones a desarrollar, así como la declaración de la lista ```productos```. Además, importa la función ```literal_eval```, que nos será útil para la el desarrollo del tercer ejercico (el menú de selección).

Para su edición, se puede usar cualquier IDE, aunque se recomienda Visual Studio Code. Para comprobar las soluciones, se proponen dos opciones. Por un lado, el fichero de plantilla incluye una
función, ```prueba_manual```, que ejecuta una serie de instrucciones para probar la funcionalidad. Este es un ejemplo de la salida cuando no se ha implementado ninguna función:

```python
Insertando 3 productos
Traceback (most recent call last):
  File "../listadelacompra.py", line 125, in <module>
    prueba_manual()
  File "../listadelacompra.py", line 93, in prueba_manual
    insertar('Desmaquillante', 4.5, ('fiesta', 'teatro'), 'Cosméticos', 5)
  File "../listadelacompra.py", line 15, in insertar
    raise NotImplementedError
NotImplementedError
```

La otra opción, es mediante el fichero ```test.py```. Este fichero se puede usar opcionalmente para comprobar que las funciones desarrolladas en la práctica funcionan correctamente, como veremos más adelante.

## Actividades de la práctica

### 1. Lista de la compra

El gestor de lista de la compra que definimos en la práctica anterior permitía productos con un formato muy sencillo: únicamente un título. En esta práctica, vamos a ampliarlo para representar cada producto como una lista con cuatro elementos:

- nombre del producto (como en la práctica anterior)
- prioridad (entero), que indica en un rango de 1 a 5 la urgencia con la que comprar este producto, siendo 1 muy poco urgente y 5 muy urgente
- precio del producto
- tupla con posibles recetas o usos que se les pueda dar al producto
- categoría del producto
- comprado (booleano) que indica si el producto ha sido comprado o no

Un posible ejemplo de producto sería:

```
producto = ['Arroz integral', 0.72, 'Alimentación', ('risotto', 'arroz a la cubana'), 3, False]
```

Las funciones a implementar para el gestor de la lista de la compra serían las siguientes:

```python
def insertar(nombre, precio, categoria, notas=(), prioridad=3):
  '''Añade un producto nuevo a la lista con los parámetros dados'''
  raise NotImplementedError

def borrar(indice):
  '''Borra de la lista el producto que se encuentra en la posición indicada'''
  raise NotImplementedError

def actualizar_precio(indice, precio):
  '''Actualiza el precio del producto con el índice dado'''
  raise NotImplementedError

def cambiar_estado(indice):
  '''Cambia el estado del producto con el índice dado entre comprado o no'''
  raise NotImplementedError

def listar_productos():
  '''Devuelve la lista de los productos'''
  raise NotImplementedError

  def mostrar_productos(comprados=True, usos=(), categorias=[]):
  '''
  Muestra por pantalla todos los productos con su información. Si un producto ya ha sido comprado, se marca con una x al comienzo.
  La prioridad se indicará mediante el uso de asteriscos (*), es decir, un artículo con prioridad 5 se representará mediante cinco asteriscos (*****).
  Si comprados es False, no se muestran los productos ya comprados.
  Usos es una tupla o lista con notas o aclaraciones. Si está vacía, se muestran
  todos los productos. Si contiene alguna nota, sólo se muestran los productos
  que tengan todas las notas proporcionadas.
  Categorias es una lista con las categorías que se quieren obtener. Si está vacía, se muestran
  todos los productos. Si contiene alguna categoría, solo se muestran los productos cuya categoría
  esté contenida en la lista.
  Ejemplo en que sólo un producto ha sido comprado:
  >>> mostrar_productos()
  [x] Alimentación - Arroz integral - *** - 0.72 € - #risotto #arroz a la cubana
  [ ] Alimentación - Huevos - * - 1.20 € - #arroz a la cubana #tortilla 
  [ ] Cosméticos - Desmaquillante - ***** - 4.50 € - #fiesta #teatro

  >>> mostrar_productos(usos=('arroz a la cubana'))
  [x] Alimentación - Arroz integral - *** - 0.72 € - #risotto #arroz a la cubana
  [ ] Alimentación - Huevos - * - 1.20 € - #arroz a la cubana #tortilla
  '''
raise NotImplementedError
```

En cada uno de estos casos, habrá que sustituir la lı́nea ```raise NotImplementedError``` por el código necesario para cumplir la funcionalidad.

_**Nota:** en temas posteriores, veremos formas más eficientes de representar información mediante la definición de clases._

### 2. Ordenación de la lista de la compra

Cuando la lista de la compra es grande, es interesante que se muestren en un orden especı́fico, y no sólo por
orden de inserción. Para ello, vamos a utilizar un algoritmo de ordenación conocido como Insertion Sort<sup>[1](#insertion_sort)</sup>, que
comparará la prioridad de cada artículo y los colocará en el orden adecuado.
El criterio de ordenación será el siguiente: una producto ha de aparecer antes que otro si su prioridad es mayor, o si el primer producto no ha sido comprado y el segundo sí.

El funcionamiento de Insertion Sort es muy sencillo: consiste en ir cogiendo uno por uno los elementos de una lista y moverlos a su posición correspondiente con respecto a los anteriormente ordenados. Así, empieza con el segundo elemento y lo ordena con respecto al primero. Luego sigue con el tercero y lo coloca en su posición ordenada con respecto a los dos anteriores, y así sucesivamente hasta recorrer todas las posiciones de la lista.

```python
def ordenar():
  '''Ordena la lista de productos en función de su prioridad, y de si han sido ya comprados o no.'''
  raise NotImplementedError
```

### 3. Menú de selección

En la práctica anterior creamos un menú interactivo utilizando varias sentencias de control. En esta
práctica, simplificaremos esta implementación mediante un diccionario. Esto nos permitirá además añadir
fácilmente una función de ayuda, que mostrará todos los comandos disponibles y la documentación de la
función python que se usa en el comando.
En particular, implementaremos los siguientes comandos:

-  ```mostrar```
-  ```insertar <nombre>; <precio>; <categoria>; <notas en formato tupla separadas por comas>; <prioridad>```
-  ```borrar <indice>```
-  ```precio <numero>; <precio>```
-  ```comprado <numero>```
-  ```ayuda```
-  ```salir```

Los cinco primeros comandos harán uso de las funciones definidas anteriormente. El comando ```ayuda``` mostrará una lista de todos los comandos disponibles, y el comando ```salir``` detendrá la ejecución del programa. En los comandos que admiten varios argumentos, estos van separados por punto y coma (;).

Para implementar este menú, usaremos un diccionario de comandos a funciones, como el siguiente:

```
{
"mostrar": mostrar_productos,
"insertar": insertar,
"borrar": borrar,
"ordenar": ordenar,
"actualizar": actualizar_precio,
"comprado": cambiar_estado,
}
```

Cada vez que el usuario lance un comando, el menú comprobará si hay una acción definida y, de ser
ası́, la lanzará con los argumentos proporcionados. En caso de insertar un comando no reconocido, el menú
mostrará un texto de ayuda, que incluirá todas las acciones definidas junto con su documentación.
La documentación de una función se puede obtener de la siguiente manera:

```
>>> mostrar_productos.__doc__.strip()
```

Por último, podemos ver que no todas las funciones tienen el mismo número de parámetros. Afortunadamente, Python permite lanzar una función con una serie de argumentos contenidos en una lista. Para ello
sólo tenemos que utilizar un asterisco antes de la lista que contiene los parámetros. Por ejemplo, el siguiente
código:

```python
>>> args = ['Desmaquillante', 4.5, 'Cosméticos', ('fiesta', 'teatro'), 3]
>>> insertar(*args)
```

es equivalente a:

```python
insertar('Desmaquillante', 4.5, 'Cosméticos', ('fiesta', 'teatro'), 3)
```

Por lo tanto, algunos posibles ejemplos del uso de este menú serían:

```
-> mostrar
-> insertar Garbanzos; 0.68; Alimentación; ('cocido', 'hummus'); 3
-> insertar Hierbabuena; 1.5; Alimentación; ('cocktails',);  1
-> mostrar
[ ] Alimentación - Garbanzos - *** - 0.68 € - #cocido #hummus
[ ] Alimentación - Hierbabuena - * - 1.5 € - #cocktails
-> comprado 0
-> mostrar
[x] Alimentación - Garbanzos - *** - 0.68 € - #cocido #hummus
[ ] Alimentación - Hierbabuena - * - 1.5 € - #cocktails
```
_**Nota:**: Los argumentos de los comandos son cadenas de texto. En algunos de los comandos (insertar, comprado o actualizar), será necesario convertirlos a enteros, float o tupla. La forma más fácil de pasar a formato numérico en nuestro caso es utilizar ```numero = int(numero)``` o ```numero = float(numero)``` dentro de la función que corresponda. Para convertir un string que representa una tupla, en una tupla, podemos usar la función ```literal_eval``` de la biblioteca ```ast```<sup>[2](#ast)</sup>._

### 4. Tareas opcionales

Como hemos dicho, hemos realizado una gestión muy básica de la lista de la compra. Por ello, se propone realizar
libremente las siguientes tareas para mejorar en el manejo de Python y obtener una gestión de lista de la compra más
útil:

- Permitir varias listas de la compra. Todo el código realizado depende de la variable ```productos``` en el módulo. Esta es una mala práctica con varias desventajas, pero la principal es que no nos permite tener más de una lista de productos. Se propone modificar el código para eliminar la variable ```productos``` y que todas las funciones reciban la lista de productos como argumento.
- Modificar el menú para que los argumentos se pidan uno a uno de manera interactiva, en lugar de
escribirlos con separadores en la misma lı́nea.
- Mostrar el ı́ndice de cada producto. Borrar o cambiar un producto requiere saber el ı́ndice del producto en
la lista. Serı́a útil que se mostrara el ı́ndice de cada producto junto con el resto de información. Existen
varios enfoques para lograrlo. Una opción es incluir el ı́ndice en el producto, igual que hemos hecho con el
resto de información, pero eso requiere modificar muchas partes del código. Una opción más elegante
es usar la función ```enumerate```, que además permite recorrer una lista (cualquier iterable) y devuelve
uno a uno los elementos y su ı́ndice.
- Añadir una función que permita borrar o modificar productos por nombre en vez de por índice.

## Evaluación
En esta tarea se incluye un fichero de pruebas llamado ```test.py```.
Su uso es opcional, pero muy recomendado, ya que permite comprobar de una manera estructurada si las funcionalidades pedidas se han implementado. Para que las pruebas se ejecuten correctamente, el fichero de la solución debe tener el nombre ```listadelacompra.py``` y estar alojado en la misma carpeta que el fichero de pruebas ```test.py```.

Los tests pueden lanzarse en cualquier momento en la línea de comando.
Si todo está bien implementado, debería obtenerse un resultado parecido a este:

```python
 $ python test.py
.....
----------------------------------------------------------------------
Ran 7 tests in 0.000s

OK
```

Si existiera algún fallo en la implementación, obtendríamos un error:

```python
$ python test.py
======================================================================
FAIL: test_cambiar (__main__.TestProductos)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "test.py", line 54, in test_cambiar
    assert (nombre == 'Huevos') == comprado
AssertionError

======================================================================
FAIL: test_precio (__main__.TestProductos)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "test.py", line 64, in test_precio
    assert (precio == 1.5) == (nombre == 'Arroz integral')
AssertionError

----------------------------------------------------------------------
Ran 7 tests in 0.001s

FAILED (failures=2)
```

## Entrega de la práctica


Para entregar la práctica, se deberá subir a Moodle en <a href="https://moodle.upm.es/titulaciones/oficiales/mod/assign/view.php?id=208688">este enlace</a> el fichero ```listadelacompra.py```, conteniendo todas las funciones requeridas en la práctica. La práctica se estar entregada en Moodle antes de las 23:59 del **12 de Noviembre de 2021**.

</br>

## Enlaces
<a name="insertion_sort">1</a>: https://en.wikipedia.org/wiki/Insertion_sort </br>
<a name="ast">2</a>: https://docs.python.org/3/library/ast.html </br>