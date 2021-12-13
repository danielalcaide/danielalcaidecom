---

title: "Definir funciones en Python"
author: "Daniel Alcaide"
date: '2021-08-05'
tags: ["python"]
categories: ["tutoriales"]
url: /definir_funciones_python
showToc: true
TocOpen: true
---

En este tutorial explicaremos cómo escribir diferentes tipos funciones personalizadas: funciones sin parámetros, funciones con parámetros únicos o  múltiples y funciones que devuelven un único o múltiples valores.

## Definición de una función

Las funciones que incorpora Python como la función `str` acepta un objeto como un número y devuelve un objeto de cadena. Si bien las funciones integradas son de mucha ayuda en nuestro trabajo diario,  a menudo, necesitaremos funciones que tengan una funcionalidad específica.

En este ejemplo vamos a ver cómo definir una función que eleva al cuadrado un número, esta función la llamaremos `square`. Para definir la función, comenzamos con la palabra clave `def`, seguida del nombre de la función (`square`).   Después del nombre añadiremos los paréntesis de abrir y cerrar y acabaremos con dos puntos. Esta primera línea de código se llama **encabezado** de función. Para completar la definición de la función, escribamos el **cuerpo** de la función elevando al cuadrado un valor, digamos 4, e imprimiendo el resultado. En este momento, nuestra función cuadrada no tiene ningún parámetro entre paréntesis. Cada vez que se llama a esta función, se ejecuta el código en el cuerpo de la función.

``````python
def square ():  # --> Encabezado
    new_value = 4 ** 2
    print(new_value)
    
square()
``````


Si quisiéramos elevar al cuadrado cualquier otro número además del 4, debemos agregar un parámetro a la definición de la función entre paréntesis. En el siguiente ejemplo, podemos ver que hemos agregado un valor de parámetro (`value`) y en el nuevo cuerpo de la función, la variable `new_value` toma el cuadrado de `value`, que luego se imprime. Ahora podemos elevar al cuadrado cualquier número que pasemos a la función al cuadrado como argumento. 

```python
def square (value):
    new_value = value ** 2
    print(new_value)
    
square(4)
```

No siempre querremos imprimir el valor resultante de la función y querremos asignar el resultado a otra variable. Para ello debemos emplear la palabra `return` de manera que ahora podremos asignar la variable `num` al resultado de nuestra función.

``````python
def square (value):
    new_value = value ** 2
    return(new_value)
    
num = square(4)
print(num)
``````

Otro aspecto esencial de las funciones personalizadas es documentar qué hacen las funciones. Esta documentación básica de las funciones se conocen como *docstrings*. Estas descripciones sirven como documentación para su función para que cualquiera que lea el *docstrings* entienda lo que hace su función, sin tener que rastrear todo el código en la definición de la función. Las cadenas de documentación de la función se colocan en la línea inmediata después del encabezado de la función y se colocan entre comillas triples.

````python
def square (value):
    """Return the square of a value"""
    new_value = value ** 2
    return(new_value)
    
num = square(4)
print(num)
````



## Múltiples parámetros de entrada y salida

A medida que vamos creando funciones más complejas necesitamos dotarlas de más parámetros de entrada. Supongamos que, en lugar de simplemente elevar al cuadrado un valor, nos gustaría elevar un valor a la potencia de otro valor que también se pasa a la función. Podemos hacer esto haciendo que nuestra función acepte dos parámetros en lugar de solo uno. Observe que ahora hay dos parámetros en el encabezado de la función en lugar de uno, `value1` y `value2`. Dentro del código de la función, el comportamiento de la función general también se modificó elevando `value1` a la potencia de `value2`. 

````python
def raise_to_power (value1, value2):
    """Raise value1 to the power of value2."""
    new_value = value1 ** value2
    return new_value
````

Podemos ejecutar la función pasando dos argumentos. El orden en el que se pasan los argumentos corresponde al orden de los parámetros en el encabezado de la función. Esto significa que cuando llamamos a `raise_to_power (2, 3)`, el número 2 se asignaría a `value1` y 3 a `value2`. 

También podemos hacer que la función devuelva varios valores. Para ello debemos utilizar objetos conocidos como **tuplas**. Una tupla es como una lista, ya que puede contener varios valores. Sin embargo, existen algunas diferencias. En primer lugar, a diferencia de una lista, una tupla es inmutable, es decir, no puede modificar los valores de una tupla una vez construida. En segundo lugar, mientras que las listas se definen utilizando corchetes, las tuplas se construyen utilizando un conjunto de paréntesis.

En el siguiente bloque de código construimos una tupla que contiene 3 elementos. La tupla se  puede descomprimir en varias variables en una línea. En este ejemplo se asigna las variables `a`, `b` y `c` a los valores de la tupla `even_nums`, en el orden en que aparecen en la tupla.

Además, también puede acceder a elementos de tupla individuales como lo hace con las listas. 

````python
even_nums = (2, 4, 6)

a, b, c = even_nums

# Elementos individuales
print(a)
print(b)
print(c)

# Elementos en tupla
print(even_nums[0])
print(even_nums[1])
print(even_nums[2])
````

Las tuplas las podemos utilizar para devolver múltiples argumentos en nuestras funciones. Por ejemplo, podemos ampliar la función anterior para que en lugar de devolver solo el valor de `value1` elevado a la potencia de `value2`, devolveremos también el valor de `value2` elevado a la potencia de `value1`. El siguiente trozo de código muestra el resultado de este cambio.

````python
def raise_both (value1, value2):
    """Raise value1 to the power of value2.
    and vice versa"""
    
    new_value1 = value1 ** value2
    new_value2 = value2 ** value1
    
    new_tuple = (new_value1, new_value2)
    
    return new_tuple

result = raise_both(2, 3)

print(result)
````

## El *scope* de los objetos en Python

Un aspecto que cobra más importancia cuando definimos funciones es el hecho del ámbito o el *scope* de los objetos. Los objetos que definimos no son siempre accesibles en cualquier lugar de un programa. Hay tres tipos de alcance:

- **Global**: objetos que están definido en el cuerpo principal de un script o un programa. 
- **Local**: un ámbito local significa que está definido dentro de una función. Una vez que se realiza la ejecución de una función, cualquier nombre dentro del ámbito local deja de existir, lo que significa que ya no puede acceder a esos nombres fuera de la definición de la función. 
- **Integrado** (*Built-in scope*): se refiere al conjunto de objetos que vienen predefinidas en Python como son `print`o `sum`.

 Cuando hacemos referencia a un objeto, primero se busca en el ámbito local y luego en el global. Si el objeto todavía no está en ninguno, se busca en el ámbito integrado.

Si aun así queremos modificar el valor de un nombre global dentro de una llamada de función local, existe la palabra clave `global` . Para ver cómo funciona, veamos el siguiente ejemplo:

````python
new_value = 10

def square ():
    """Return the square of a value"""
    global new_value
    new_value = new_value ** 2
    return(new_value)
    
print(square())
print(new_value)

# 100
# 100 <-- New value se ha actualizado con el valor de la función
````

Dentro de la función, usamos la palabra clave `global` seguida del nombre de la variable que queremos acceder y modificar. En el ejemplo modificamos `new_value` a su cuadrado. 

De manera similar, en una función anidada puede usar la palabra clave `nonlocal` para crear y cambiar valores en el ámbito al que esta adjunto. En el siguiente bloque modificamos el valor de `n` en la función `inner`; como estamos usando la palabra clave `nonlocal`, también alteramos el valor de `n` en el el nivel superior, dentro del ámbito de la función `outer`.  Al llamar a la funció `outer` imprime el valor de `n` como se define dentro de la función `inner`.

````python
def outer():
    """Prints the value of n."""
    n = 1
    
    def inner():
        nonlocal n
        
        n = 2
        print(n)
    
    inner()
    print(n)
    
outer()

# Devuelve:
# 2
# 2
````



## Argumentos por defecto y flexibles

A menudo nos interesa definir funciones con argumentos predeterminados, en Python  este tipo de argumentos se definen de manera similar a otros lenguaje, en el encabezado se define el parámetro y se añade un signo igual y el valor de argumento predeterminado. 

````python
def power(number, pow=1): 
    ...
 
# Podemos definir valores especificos para pow 
# o utilizar el valor por defecto
power(9, 2) # 81
power(9) # 9
````

Además de los **argumentos por defecto**, podemos escribir funciones sin especificar el número de argumentos conocidos como **argumentos flexibles**. Para ello, debemos usar el símbolo `*` en el encabezado seguido del parámetro que usaremos en la función (`args` en el ejemplo) . Esto hará que que todos los argumentos pasados en la función los entienda como una **tupla** y  use el el argumento `args` como tal dentro del cuerpo de la función. 

En el siguiente ejemplo mostramos un función que toma un número indefinido de de número y los suma. Vea como el argumento `args` es la tupla que se recorre en el bucle `for`. 

````python
def add_all(*args):
    """Sum all values in *args together."""
    
    # Initialize sum
    sum_all = 0
    
    # Accumulate the sum
    for num in args:
        sum_all += num
        
    return sum_all

print(add_all(1, 2)) 			# 3
print(add_all(5, 10 , 15, 20))	# 50
````

De manera parecida, puede usar el doble símbolo `**`  seguido de un parámetro (`kwargs` en el ejemplo) para definir un número arbitrario de argumentos de palabras **clave-valor**. En el cuerpo de la función, el argumento lo entenderá como un **diccionario**.

En el siguiente ejemplo definimos una función para imprimir todos los pares clave-valor pasados como argumentos.

````python
def print_all(**kwargs):
    """Print out key-value pairs in **kwargs."""
    
    # Print out the key-value pairs
    for key, value in kwargs.items():
        print(key +  ":"  + value)

print_all(name="dumbledore", job="headmaster")
# name:dumbledore
# job:headmaster
````

Tenga en cuenta que no son los nombres `args` y `kwargs` los que son importantes cuando se usan argumentos flexibles, sino que están precedidos por el símbolo `*` simple y  `**` doble, respectivamente.


 ## Funciones anónimas

A pesar que hasta ahora hemos creado todas las funciones utilizando la palabra clave `def`, existe una forma más rápida de escribir funciones en solamente una línea. Este tipo de funciones se conocen como funciones lambda porque utilizan la palabra clave `lambda`. En el siguiente bloque reescribimos la función de `raise_to_power` como una función lambda. 

````python
raise_to_power = lambda x, y: x ** y

raise_to_power(2, 3)
# 8
````

Como se ve en la declaración de la función, después de la palabra clave `lambda`, especificamos los nombres de los argumentos, tras los dos puntos especificamos la expresión que deseamos que devuelva. Las funciones lambda nos permiten escribir funciones de una manera rápida aunque dificulte la legibilidad del código. Sin embargo en ocasiones pueden ser muy útiles, en las funciones  como `map` y  `filter`. Por ejemplo, las función `map` sigue la siguiente sintaxis, `map(función, secuencia)` y ejecuta la función especificada iterativamente sobre la secuencia, como una lista.  Podemos pasar funciones lambda dentro del `map` convirtiendo la función en una función anónima. En el siguiente ejemplo, usamos `map`  con una función lambda que eleva todos los elementos de una lista y almacenaremos el resultado en el objeto `square_all`. Al imprimir el objeto `square_all` el sistema nos revela que en realidad es un objeto de mapa, por lo que para ver qué contiene, usamos la función `list` para convertirlo en una lista e imprimir los resultados.

````python
nums = [48, 6, 9, 21, 1]

square_all = map(lambda num: num ** 2, nums)

print(square_all)
# <map object at 0x00000188929E4A30>

print(list(square_all))
# [2304, 36, 81, 441, 1]
````


 ## Manejo de errores

Cuando usamos una función incorrectamente, ésta debería arrojarnos un error. Por ejemplo, si pasamos el argumento incorrecto a la función `float` con el parámetro de entrada `hola`. Python me dará un error diciéndome que no puede convertir la cadena de texto en un número. 

````python
float('hola')

# ---------------------------------------------------------------------------
# ValueError                                Traceback (most recent call last)
# <ipython-input-13-fd4cbaf57f0b> in <module>()
# ----> 1 float('hola')
# 
# ValueError: could not convert string to float: 'hola'
````

Cuando escribimos nuestras propias funciones, es posible que deseemos detectar problemas específicos y escribir mensajes de los errores. Por ejemplo, en la siguiente función que calcula una función de la raíz cuadrada, queremos que el sistema nos indique un error cuando el parámetro de entrada sea erróneo. Los problemas que el sistema se encuentra durante el ejecución se conocen como *excepciones*. La manera de detectar excepciones es utilizando la combinación de `try-except` de Python. Durante el proceso `try` el sistema intenta ejecutar el código, en caso de no poder ejecutarlo debido a una excepción, Python ejecuta la parte especificada en en el `except`.

````python
def sqrt (x):
    """Return the square root of a value"""
    try:
      return x ** 0.5
    except:
      print('X must be an int or float')
    
sqrt('hola')
# X must be an int or float
````

Es posible que queramos solamente detectar un tipo específico de errores, por ejemplo, identificar errores en la clase del parámetro de entrada. Para ello debemos en la excepción al tipo que corresponde. 

````python
try:
	# ...
except TypeError:
    print('X must be an int or float')
````

En lugar de imprimir mensajes de error, también podríamos querer generar un error utilizando la palabra `raise`. Por ejemplo, nuestra función de raíz cuadrada devuelve un número complejo que es posible que no queramos. En el siguiente ejemplo utilizamos la condición `if` para filtrar los valores negativos y mostrar un error de valor con la instrucción `ValueError`:

````python
def sqrt (x):
    """Return the square root of a value"""
    if x < 0:
      raise ValueError('x must be non-negative')

    return x ** 0.5
    
sqrt(-2)
# ---------------------------------------------------------------------------
# ValueError                                Traceback (most recent call last)
# <ipython-input-24-516cda378b80> in <module>()
#      6     return x ** 0.5
#      7 
# ----> 8 sqrt(-2)
# 
# <ipython-input-24-516cda378b80> in sqrt(x)
#      2     """Return the square root of a value"""
#      3     if x < 0:
# ----> 4       raise ValueError('x must be non-negative')
#      5 
#      6     return x ** 0.5
#
# ValueError: x must be non-negative
````



