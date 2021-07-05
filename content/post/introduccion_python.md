---

title: "Introducción a Python"
author: "Daniel Alcaide"
date: '2021-07-05'
tags: ["python"]
categories: ["tutoriales"]
url: /introduccion_python
showToc: true
TocOpen: true
---

## ¿Qué es Python?

Es un lenguaje de programación muy versátil que permite desarrollar casi cualquier tipo *software* y que puede ser ejecutado en casi cualquier dispositivo. Una de sus mayores fortalezas es su gran comunidad que ha ayudado a extender las posibilidades de este lenguaje creando paquetes de funciones que facilitan muchísimo el desarrollo de nuevo programas. Como no podría ser de otra manera, también encontramos un inmensa cantidad de paquetes específicos para ciencia de datos. 

Existen muchos tutoriales para instalar Python, en realidad para análisis de datos los más recomendable es usar Anaconda que es un distribución de Python que incluye la mayoría de liberarías que necesitaremos. [Aquí](https://www.youtube.com/watch?v=OmmklYlRGzo) os dejo un tutorial para instalarlo.

## ¿Dónde escribo el código?

podemos destacar tres maneras de escribir código en Python:

- **IPython Shell**: La *shell* de Python (comando `ipython` en nuestro terminal), es un lugar donde puede escribir código Python y ver inmediatamente los resultados de manera interactiva
- **Archivos `.py`**: Estos son los scripts, archivos de texto con la extensión `.py`. Son básicamente una lista de comandos de Python que se ejecutan, casi como si estuviera escribiendo los comandos en la *shell*, línea por línea.
- **Jupyter notebook**: Es un entorno de desarrollo que combina la programación interactiva como IPython con la documentación a modo de informe. Esta herramienta se estructura en bloques tanto de código en Python como de texto usando la sintaxis *markdown*. 

## Lo más básico del lenguaje Python 

En esta sección resumimos las características más básicas del lenguaje que nos facilitarán comenzar a programar:

- Los comentarios en el texto se ponen usando el símbolo `#`.

- Devolver mensajes en un script o dentro de una función se consigue con la función `print()`.

- Las variables tienen cuatro tipos diferentes: `float` (número decimales), `int` (números enteros), `str` (cadenas de texto) y `bool` (variables lógicas `True` o `False`). La función que devuelve el tipo de variable es la función `type`.

- Las tipos de variables se pueden cambiar de tipo utilizando su función correspondiente, por ejemplo, la función `str()` convertirá esta variable a texto. Lo mismo puede suceder con la función `float()`para convertir texto a un número.  

- Los operadores se comportan diferentes según el tipo de variable. Por ejemplo, si sumamos dos *strings*, el operados `+` concatenará estas cadenas de texto. 

- Los operadores para comparar expresiones son las siguientes:

  | Operadores | Significado   |
  | ---------- | ------------- |
  | `<`        | menor que     |
  | `<=`       | menor o igual |
  | `>`        | mayor que     |
  | `>=`       | mayor o igual |
  | `==`       | igual         |
  | `!=`       | no igual      |

## Listas

Para trabajar con varias medidas como, por ejemplo, la altura de varias personas y almacenar esta información en una única variable se pueden utilizar las listas. Las listas se definen entre corchetes (`[a, b, c]`) y pueden contener múltiples tipos de elementos dentro de la misma lista, es decir, podríamos definir una lista con esta estructura de elementos `[str, float, bool, str]` o incluso hacer una lista de listas.

Python utiliza índices para acceder al contenido de la lista. La primera posición de la lista se establece con le índice en la posición 0. Por  ejemplo, acceder al cuarto elemento de la lista `a` necesita establecer el índice en la tercera posición `a[3]`. También se puede especificar números negativos como índices. Esto es útil para acceder a una lista empezando por el final de la misma. Por ejemplo, la última posición de la lista `a` sería `a[-1]`. 

Además de acceder a elementos específicos, también podemos seleccionar subconjuntos de listas definiendo un intervalo. En la lista `a` la selección del subconjunto `a[3:5]` devuelve al cuarta y la quinta posición de la lista pero no la sexta, es decir devuelve desde donde comiencuandoza (`start`) pero no devuelve la posición donde acaba (`stop`) definiendo `a[ start : stop ]`. También se puede no especificar el índice al principio o al final de intervalo, por ejemplo:

- `a[:5]` en este caso entiende que tiene que mostrar todos los valores desde la posición 0
- `a[3:]` mostrará todos los índices desde la cuarta posición hasta el final de la lista. 
- `a[:]` mostrará todos los elementos de la lista.

Con las listas seleccionadas, las acciones que podemos hacer son: cambiar elementos de la lista, añadir elementos nuevos o eliminar los existentes:

- **Cambiar elementos:** A partir de los mismos corchetes que hemos usado para subconjuntos de listas, asignamos nuevos elementos usando el signo igual. Por ejemplo, podemos asignar el valor `1.86` al sexto elemento lista `a` de manera que `a[5]=1.86` o podemos modificar varios elementos a la vez seleccionando y reasignado subconjuntos en las listas. En este caso modificamos los dos primeros elementos de la lista `a` asignándole una lista del mismo tamaño, es decir,  `a[0:2] = ["lisa", 1.74]`
- **Añadir nuevos elementos:** Cuando se utiliza el signo `+` en  dos listas, Python simplemente pega su contenido en una sola lista. Si queremos concatenar la lista añadir el contenido de la lista `a` a la lista `b` tendríamos que especificar: `a = a + b`.
- **Eliminar elementos:** Para eliminar uno o varios elementos tendremos que especificar la selección a eliminar dentro de la función `del`. Por ejemplo, si queremos eliminar el tercer elemento de la lista `a` tendríamos que declarar `del(a[2])`.

## Funciones

Una función es un trozo de código reutilizable que resuelven una tarea particular. Por ejemplo, si queremos obtener el máximo de una lista `x = [1,3,5,8]` podemos utilizar la función `max(x)` que ya viene integrada en el lenguaje. Otra de estas funciones que vienen integradas en el lenguaje es `round`. En este caso, esta función necesita especificar dos parámetros, el primero el número que a redondear y el segundo el número de de dígitos detrás del punto decimal. De manera que si queremos redondear el número 1.68 a solamente un decimal podemos usar `round(1.68, 1)`. Tenga en cuenta que los múltiples parámetros se separan por comas. 

## Métodos

Podemos explicar los métodos como funciones que pertenecen a objetos en Python. Un objeto Python de tipo cadena tiene métodos, como el método `capitalize()` que convierte la cadena en mayúsculas o el método `replace()` que remplaza un conjunto de caracteres por otros. Las listas tienen sus propios métodos como el método `index` que permite encontrar la posiciones de estos elementos. 

Suponga que quiere identificar la palabra *manzana* dentro de la lista `a = ["tomate", "fresa", "manzana"]`. Para llamar al método `index` utilizaremos el punto para unir el objeto y el método, de manera que `a.index("manzana")` debería devolver el índice 2. 

Tenga en cuenta que el método `index` también existe en los objeticos de tipo carácter (`str`), sin embargo, éste busca la posición del carácter. 

## Paquetes

Los paquetes sirven para extender las funcionalidades de Python con funciones, tipos de objetos y métodos creados para resolver problemas particulares. Se estructuran como un directorio de scripts donde cada uno de ellos especifica un subconjunto de todas las funcionalidades el cual se conoce como módulo. 

Hay miles de paquetes de Python disponibles en Internet. Entre ellos se encuentran los paquetes para la ciencia de datos: `numpy` para trabajar de manera eficiente con matrices, `matplotlib` para la visualización de datos o `scikit-learn` para el aprendizaje automático. 

No todos estos paquetes están disponibles en Python de forma predeterminada. Para usar paquetes de Python, primero tendrás que instalarlos en tu propio sistema y luego poner en el código unos comandos para decirle a Python que desea usar estos paquetes. 

Para facilitar el proceso de instalación podemos utilizar el programa `pip`, un sistema de mantenimiento de paquetes para Python. Si lo tenemos instalado podemos ejecutar el comando `pip3 install numpy` e instalar en nuestro sistema el paquete `numpy`. 

Antes de poder utilizar las funcionalidades de este paquete debemos importarlo en nuestro script. Tenemos varias opciones:

- Importar el módulo e utilizar el nombre del mismo para acceder a sus funciones. 

  ````python
  import numpy
  numpy.array([1, 2, 3])
  ````

- Importar el módulo e utilizar un alias del mismo.  

  ````python
  import numpy as np
  np.array([1, 2, 3])
  ````

  El alias `np` nos permite escribir menos en nuestro desarrollo y esto hace que la lectura del código sea más sencilla. 

- Importar una función del paquete.  

  ````python
  from numpy import array
  array([1, 2, 3])
  ````

  De esta manera solamente estaríamos importando la función `array` del paquete `numpy`. 

## Numpy

El paquete de Python Numpy ofrece grandes funcionalidades para el manejo de de listas y matrices y así facilitar la manipulación de datos. Por ejemplo, operaciones como la división están implementadas por defecto en este tipo de objetos.

```python
height = [1.73, 1.68, 1.71, 1.89, 1.79]
weight = [65.4, 59.2, 63.6, 88.4, 68.7]

# La siguiente operación devuelve este error: 
# TypeError: unsupported operand type(s) for **: 'list' and 'int'
weight / height ** 2

# Sin embargo con Numpy podemos realizarlo:
np_height = np.array(height)
np_weight = np.array(weight)
np_weight / np_height ** 2array

# Devolviendo el resultado
([ 21.852,  20.975,  21.75 ,  24.747,  21.441])

```

Debemos tener en cuenta que Numpy puede hacer todo esto tan fácilmente porque asume que su matriz Numpy solo puede contener valores de un solo tipo. Por ejemplo, una matriz numérica o de boléanos.

Además de las funcionalidades para la manipulación de datos, Numpy ofrece métodos que nos permiten calcular estadísticos, por ejemplo `np.mean()`, `np.median()`, `np.std()`, etc.

## Matplotlib

Existen muchos paquetes en Python para visualizar datos pero Matplotlib es uno de los mas populares. La creación de gráficos es sencilla, por ejemplo, tenemos la función `plot()` que nos genera un gráfico automáticamente a partir de dos variables uniendo cada combinación de puntos con una línea:

```python
import matplotlib.pyplot as plt

year = [1950, 1970, 1990, 2010]
pop = [2.519, 3.692, 5.263, 6.972]
plt.plot(year, pop)
plt.xlabel('Year')
plt.ylabel('Population')
plt.title('World Population')
plt.show()
```

![Matplotlib plot function](/post/introduccion_python/matplotlib_plot.png)

Un gráfico de utilizad es el diagrama de dispersión, Matplotlib también incluye esta función. Para rehacer con este tipo de gráfico, solamente tendríamos que substituir la función `plot`por la función `scatter`. De la misma manera, podemos crear histogramas con la función `hist` para explorar la distribución de una variable numérica.

## Diccionario

Los diccionarios en Python son estructuras de datos que permiten almacenar datos como pares de clave-valor al igual que sucede en como con los diccionarios convencionales donde tenemos la palabra (clave) y la definición (valor). Por ejemplo: 

````python
world = {"afghanistan":30.55, "albania":2.77, "algeria":39.21}

# La siguiente instrucción devuelve el valor 
# 2.77 que corresponde a la clave albania 
world["albania"]

# Para ver todas la claves en un diccionario 
# podemos utilizar el método .keys()
world.keys
# --> dict_keys(['afghanistan', 'albania', 'algeria'])

# Para añadir o eliminar ( del() ) elementos al diccionario 
# podemos accerlo de manera similar a las listas
world["sealand"] = 0.0028
````

Como se puede ver en la imagen anterior, los diccionarios de definen entre llaves (`{ }`) donde se incluye los pares clave-valor separados por comas. Ten en cuenta que las claves en un diccionario son únicas y si se añaden claves repetidas solamente se mantendrá la última.

## Pandas

El paquete Pandas nos presenta la posibilidad de estructurar los datos como DataFrames, un tipo de datos que podemos encontrar de igual manera en R.  El formato de un DataFrame es muy sencilla, las filas representan las observaciones y las columnas representan las variables.

Para crear un  DataFrame existen diferentes métodos, lo podemos hacer desde un diccionario `pandas.DataFrame()` pero lo más habitual será utilizar un archivo o base de datos. En este ejemplo utilizaremos un archivo CSV donde importaremos el archivo [brics.csv](/post/introduccion_python/brics.csv)

````python
import pandas as pd

brics = pd.read_csv("brics.csv", index_col = 0)
print(brics)

# Nota: el parámetros index_col = 0 nos permite 
# indicar que la primera columna contiene los índices 
# de las filas
````

El resultado de esté será la tabla que hemos leído.

````
	country			capital		area	population
BR	Brazil			Brasilia	8.516	200.40
RU	Russia			Moscow		17.100	143.50
IN	India			New Delhi	3.286	1252.00
CH	China	 		Beijing		9.597	1357.00
SA	South Africa		Pretoria	1.221	52.98
````

Para seleccionar un subconjunto de de filas o columnas tenemos que utilizar los corchetes (`[ ]`). Pandas solo acepta:

- un nombre de columna o una lista con los nombres de varias columnas. 
- un subconjunto de filas o una condición booleana.

Por tanto para seleccionar la columna `country`y `capital`tenemos que utilizar la instrucción `brics[["country", "capital"]]` y para seleccionar los primero cuatro filas de la tabla `brics[0:4]`. 

Las funciones de `loc`y `iloc` nos facilita la selección de elementos en un DataFrame. `loc` se utilizar para seleccionar utilizando las etiquetas y `iloc` es el equivalente para la selección basado en posiciones. Por ejemplo:

````python
# Podemos seleccionar filas usando .loc
brics.loc[["RU", "IN", "CH"]]
````

donde se mostrarán la filas correspondientes:

``````
country		capital		area	population
RU	Russia	Moscow		17.100	143.5
IN	India	New Delhi	3.286	1252.0
CH	China	Beijing		9.597	1357.0
``````

También podemos filtrar filas y columnas a la vez añadiendo un coma tras la selección de filas, `brics.loc[["RU", "IN", "CH"], ["country", "capital"]]` o  seleccionar solamente filas  incluyendo todas las filas `brics.loc[:, ["country", "capital"]]`. 

La función `iloc` funciona de manera similar y podríamos realizar las mismas selecciones que antes usando las posiciones, por ejemplo `brics.iloc[[1, 2, 3]]` para seleccionar solamente filas, `brics.iloc[[1, 2, 3], [0, 1]]` para filas y columnas, y  `brics.iloc[:, [0, 1]]` para solamente columnas. 

## Operadores 

Además de los operadores de relación como el `>` o el `==`, éstos los podemos combinar usando los operadores lógicos, los tres más comunes son `and`, `or` y `not`. Las matrices y listas en Numpy no soportan estos operadores ya que normalmente intentaremos comparar múltiples elementos y los operadores básicos no están diseñados para tal propósitos. Para ello, existen las funciones `logical_and()`,  `logical_or()` y `logical_not()`. 

````python
import numpy as np
height = np.array([1.73, 1.68, 1.71, 1.89, 1.79])

# Evalúa si cumplen la condición
print(np.logical_and( height >= 1.70, height <= 1.80))

# Muestra los valores 
print(height[np.logical_and( height >= 1.70, height <= 1.80)])
````

Cuando queremos realizar acciones según las condiciones, tenemos los operadores condicionales como `if`, `else` y `elif`.

### `if`

Tras la instrucción `if` tenemos que indicar la condición a evaluar y añadir dos puntos al final. Si cumple la condición el código se ejecutará. En el siguiente ejemplo se mostrarán los dos impresiones por pantalla. Tenemos que recordar que las acción tras el operador de condición (`if`, `else` y `elif`) deben estar indicadas ya sea por un tabulador o por cuatro espacios. Con el IDE (*Integrated Development environment*) que utilicemos o el notebook ya nos realizará esto automáticamente, pero no está de más tenerlo en cuenta.  Para continuar con el código sin incluirlo en el `if` simplemente dejaremos de incluir acciones tabuladas o con espacios. 

````python
z = 6
if z % 2 == 0 :    # False    
    print("checking "  + str(z))    
    print("z is even")
# Devuelve "checking 6" y "z is even"
````

### `else`
La instrucción `else` se ejecuta si la condición `if`no se cumple. Como vemos en el ejemplo siguiente, la expresión `else`no hace falta especificar una condición.

````python
z = 5
if z % 2 == 0 :    # False    
    print("z is even")
else :    
    print("z is odd")
# Devuelve "z i odd"
````

### `elif`

Cuando necesitamos un comportamiento aún más personalizado tenemos las opción de incluir uno o varios `elif`. Éste sirve para incluir cadenas de condiciones que necesitan ser evaluadas. 

````python
z = 9
if z % 2 == 0 : 
    print("z is divisible by 2")    # False
elif z % 3 == 0 : 
    print("z is divisible by 3")    # True
else :
    print("z is neither divisible by 2 nor by 3")
````

## Bucle

En esta sección repasaremos como definir bucles en Python, como son `while`, 

### `while`

El bucle definido por la instrucción `while` es algo similar a una instrucción `if`, ejecuta el código interno si la condición es verdadera. Sin embargo, a diferencia de la instrucción `if`, el bucle `while` continuará ejecutando este código una y otra vez siempre que la condición sea verdadera. La sintaxis de un bucle `while` es muy similar a la instrucción `if`, como puede ver en el siguiente ejemplo: 

````python
# Definimos un valor inicial
error = 50.0

# La condición se evalúa hasta 
# que se cumpla la condición
while error > 1:     
    error = error / 4      
    print(error)
````

### `for`

El bucle `for` se ejecuta un número determinado por una secuencia. Por ejemplo, en el bucle siguiente, se imprime el valor de la variable `height` que se va actualizando en cada iteración recorriendo la lista `fam`.

``````python
fam = [1.73, 1.68, 1.71, 1.89]

for height in fam :     
    print(height)
# 1.73
# 1.68
# 1.71
# 1.89
``````

La función `enumerate()` dentro de un bucle `for` nos permite acceder a dos valores de la lista, primero a los valores de la lista y segundo a los índices de la misma. Para utilizar esta función debemos modificar algo el bucle anterior e incluir dos variables  dentro de la definición del `for`, la variable `index` y la variable `height`: 

````python
fam = [1.73, 1.68, 1.71, 1.89]

for index, height in enumerate(fam) :    
    print("index " + str(index) + ": " + str(height))
# index 0: 1.73
# index 1: 1.68
# index 2: 1.71
# index 3: 1.89
````

 El bucle `for`no solo funciona con listas y también podemos crear un bucle que recorra los caracteres de una cadena. 

Para recorrer diccionarios en un bucle `for` debemos utilizar el método `.items()` de manera que la primera línea de bucle sería algo como: 

````python
for key, val in my_dict.items() :
    ...
````

En cambio, para recorrer listas de Numpy debemos utilizar la función `.nditer()` y el bucle quedaría algo como esto:

````python
for val in np.nditer(my_array) :
    ...
````

Durante el análisis de datos los bucles más comunes serán sobre los DataFrame de Pandas. Si definimos un bucle iterando el DataFrame como si fuera un lista, el bucle mostrará las etiquetas de las columnas (ver Ejemplo 1). 

````python
import pandas as pd

brics = pd.read_csv("brics.csv", index_col = 0)

# 		country			capital		area	population
# BR	Brazil			Brasilia	8.516	200.40
# RU	Russia			Moscow		17.100	143.50
# IN	India			New Delhi	3.286	1252.00
# CH	China	 		Beijing		9.597	1357.00
# SA	South Africa	Pretoria	1.221	52.98

# Ejemplo 1: Itera las las columnas 
for val in brics :
    print(val)
# country
# capital
# area
# population    
````

Para iterar sobre las filas, debemos utilizar el método `.iterrows()`. Este método proporciona dos piezas de datos, las etiquetas (variable `lab` en el siguiente ejemplo) y los valores de las filas del DataFrame (variable `row` del ejemplo). En la primera iteración del mostrará por tanto, la etiqueta `BR` guarda en la variable `lab`y el objeto correspondiente a la fila de `Brazil` en la variable `row`. 

````python
# Ejemplo 2: Itera las filas
for lab, row in brics.iterrows():    
    print(lab)    
    print(row)
# El primer print muestra el rowname
# El segundo print muestra los valores de la fila
````

En el tercer ejemplo mostramos como crear una nueva columna dentro del bucle. En el podemos ver como podemos combinar los otros métodos y funciones  dentro del bucle.

````python
# Ejemplo 3: Crea un nuevo valor en cada iteración
for lab, row in brics.iterrows() :  
    brics.loc[lab, "name_length"] = len(row["country"])
print(brics)  
````

No obstante,  la creación de de esta variable dentro de un bucle no es para nada eficiente y para ello disponemos de métodos como `apply`que además de simplificar la creación de la columna, facilitar la lectura del código, es más eficiente que el bucle `for`. 

````python
# Ejemplo 4: Ejemplo 3 de manera optimzada
# método apply
brics["name_length"] = brics["country"].apply(len)
print(brics)
````

