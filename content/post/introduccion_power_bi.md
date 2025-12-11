---
title: "Introducción a Power BI"
author: "Daniel Alcaide"
date: '2021-04-28'
tags: ["power bi"]
categories: ["tutoriales"]
url: /introduccion_powerbi
showToc: true
TocOpen: true
draft: true
---

> Este tutorial esta creado a partir de mis notas del curso de *Introduction to Power BI de DataCamp* 

## ¿Qué es Power BI?

Power BI es una herramienta que le permite crear informes interactivos con los que explorar datos de para obtener información. 

Power BI tiene dos versiones,  la versión de escritorio ([Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/)) y  la versión en la nube ([Power BI Online](https://app.powerbi.com/)). Power BI Desktop es una herramienta de creación de informes y análisis de datos disponible en tu equipo local. Es la mejor manera de crear informes ya que es la versión que más funcionalidades incluye como el como el Query Editor. Por otro lado, Power BI Online también nos permite crear informes pero de una manera más limitada. Por lo general, los informes se crean en local y luego se publican en el versión online para que puede ser accedido por otros usuarios o compañeros.   

En este tutorial trabajaremos únicamente con la versión de Power BI Desktop

## Interfaz Power BI Desktop

La interfaz de Power BI se puede dividir en tres vistas: 

1. Vista de informe: La vista de informe es la vista predeterminada. En esta vista, puedes crear informes y elementos visuales.
2. Vista de datos: Puedes ver los datos utilizados en el modelo de datos asociado con su informe.
3. Vista de modelo: Puedes ver y administrar las relaciones entre tablas en su modelo de datos.

![Power BI Desktop](/post/introduccion_power_bi/power_bi_desktop.png)

## El primer informe en Power BI

Para crear el primer informe, necesitamos unos datos sobre los que realizar los gráficos. En este tutorial utilizaremos la base de datos de muestra de [Wide World Importers (WWI)](WorldWideImporters.zip) que simula las importaciones y distribuciones de una empresa. Este conjunto de datos esta compuesto por los siguientes archivos: 

````bash
DimCity.csv
DimCustomer.csv
DimDate.csv
DimEmployee.xlsx
DimStockItem.csv
FactSale.csv
````

### Cargar datos en Power BI 

En este ejemplo vamos a cargar el primer los ficheros `FactSale.csv`y `DimEmployee.xlsx` y vamos a hacer la primera visualización interactiva. Para cargar estos ficheros debemos utilizar el botón **Obtener datos** como se muestra en la imagen. Empezaremos con archivo `FactSale.csv`. 

![Cargar datos en Power BI](/post/introduccion_power_bi/cargar_datos_power_bi.png)

### Gráfico de barras

Una vez cargado el archivo veremos en la parte derecha de la pantalla todos los campos disponibles. Simplemente arrastrando el campo `Total Excluding Tax` al canvas, Power BI entenderá que es una variable numérica y generará una representación gráfica de esta variable. 

![Añadir campos a Power BI](/post/introduccion_power_bi/añade_campos_power_bi.gif)

### Relaciones entre tablas

Está la vista de datos, donde podemos examinar nuestros datos sin procesar, hay varias columnas que se refieren a claves, por ejemplo, esta columna llamada `Salesperson key`. 

Para poder tener más información sobre estos vendedores cargaremos el archivo `DimEmployee.xlsx` tal y como hemos hecho anteriormente seleccionando archivo Excel. La tabla `DimEmployees` es una tabla de dimensiones que contiene más información sobre el vendedor para cada transacción. 

Podemos ver la tabla `DimEmployee` ahora en la vista de datos y el panel de campos. Hay varias columnas, incluida una llamada `Employee Key`. En la vista del modelo podemos establecer relaciones entre los datos que cargamos. En este ejemplo conectaremos la variable `Salesperson key` de `FactSale`con la variable `Employee Key` de la tabla `DimEmployees` arrastrando una variable a la otra tal y como se muestra en la siguiente animación. 

![Crear relaciones en Power BI](/post/introduccion_power_bi/relaciones_power_bi.gif)

Una vez creada la relación Power BI es consciente de que existe una relación entre los dos archivos diferentes que hemos cargado. Regresemos a la vista de informes. Ahora agreguemos la variable `Employee` al diagrama de barras arrastrando éste al elemento **Eje** del gráfico de manera que quede algo así .

![Diagrama barras Power BI](/post/introduccion_power_bi/diagrama_barras_power_bi.png)

### Creando el dashboard

Para añadir más elementos que complementen al gráfico de barras podemos hacerlo seleccionando las visualizaciones que nos interesen del panel de visualizaciones. Como ejemplo vamos a añadir una tarjeta que resuma el `Total Excluding Tax` al informe, para ello hacemos clic en la parte en blanco de la pantalla y seleccionamos la visualización tarjeta y agregamos al variable  `Total Excluding Tax`

![Tarjetas en Power BI](/post/introduccion_power_bi/tarjeta_power_bi.png)

Una de las ventajas de Power BI es que crea relaciones automáticamente entre las visualizaciones convirtiendo el dashboard en interactivo. Por ejemplo, seleccionando cualquiera de las barras, la tarjeta cambiará automáticamente filtrando solamente esos datos.  Para anular la selección podemos volver a clicar en el área en blanco del canvas. 

Por otro lado, también podemos enriquecer las visualizaciones añadiendo nuevas variables a los gráficos. Por ejemplo, en la imagen siguiente se ha añadido la variable `Profit` (en el campo **Valores**) al diagrama de barras. Al tener las dos variables en el mismo gráfico podemos comparar fácilmente las dos variables. 

![Nuevas variables en el gráfico de barras](/post/introduccion_power_bi/nuevas_variables.png)

Ten en cuenta que Power BI en los variables numéricas muestra la suma pero no siempre nos interesará mostrar esta agregación. A veces nos interesa mostrar el valor medio o el recuente de elementos. Para ello podemos modificar la agregación clicando sobre el símbolo **V** que aparece al lado de la variable en el campo **Valores**. 

![Modificar valor agregado Power BI](/post/introduccion_power_bi/modificar_valor_agregado_power_bi.png)

## Dando formato a los informes de Power BI

El formato de nuestras visualizaciones es importante para facilitar la interpretación de quien las utiliza. En los siguientes apartados se muestran soluciones de problemas que nos podemos encontrar creando nuestro informes. 

### Ordenar variables 

Es común tener información agregada a nivel mensual. Por defecto, Power BI no va entender que la palabra *Enero*, *Febrero*, *Marzo*, etc. corresponde a los mese y por tanto solamente vamos a poder ordenar estos datos alfabéticamente, (tanto de manera ascendente o descendente). Por ejemplo, os muestro el siguiente caso:  

![Eje desordenado Power BI](/post/introduccion_power_bi/eje_desordenado_power_bi.png)

Para solucionar este problema tenemos que indicarle a Power BI el orden de estos datos. Para ello nos tenemos que ir la vista de datos, clicar sobre el botón **Ordenar por columna** y seleccionar la columna que nos indique el order. En este caso la columna que determina el orden es la la variable numérica del mes.

![Ordenar variables Power BI](/post/introduccion_power_bi/ordenar_variables_power_bi.gif)

Si volvemos a la vista de informe veremos que los meses ahora están ordenados de manera adecuada.

![Eje ordenado Power BI](/post/introduccion_power_bi/eje_ordenado_power_bi.png)

### Desglosar y profundizar en los datos

A veces puede ser útil revelar detalles adicionales al profundizar en nivel menos agregado de los datos. Desglosar permite que un solo objeto visual muestre datos en un nivel alto y luego le da al usuario la opción de ver los datos en un nivel más detallado. Esta acción es posible mediante la creación de jerarquías. Un ejemplo de jerarquía podría ser Año > Trimestre > Mes > Día 

Una vez que se crea una jerarquía, puede navegar hacia arriba y hacia abajo a niveles inferiores. Hay maneras diferentes de hacer esto. Power BI tiene un conjunto de controles de exploración que le permiten ver los datos de diferentes formas. En el siguiente ejemplo, usamos un gráfico de columnas que tiene una jerarquía formada por año, trimestre y mes. 

<img src="/post/introduccion_power_bi/diagrama_barras_agregado_power_bi.png" alt="Diagrama barras agregado Power BI" style="zoom:50%;" />

Al seleccionar el icono de flechas dobles, se profundiza en todos los campos a la vez. Te lleva al siguiente nivel en la jerarquía. Si está mirando el nivel del año,
puede desglosar hasta el nivel de un trimestre para todos los años, y luego a nivel mensual para todos los años. Ten en cuenta que las cantidades que ve aquí son las cantidades de ventas por mes para todos los años. Entonces, el monto de enero es el total de enero de 2017, 2018 y 2019, sumados.

<img src="/post/introduccion_power_bi/diagrama_barras_agregado2_power_bi.png" alt="Diagrama barras agregado por trimestre Power BI" style="zoom:50%;" />

## El lenguaje DAX para Power BI

DAX es el lenguaje de cálculo utilizado en Power BI. Proporciona la capacidad de crear columnas, tablas y medidas generadas mediante programación. Si alguna vez ha utilizado fórmulas y funciones de Excel, el lenguaje DAX está inspirado en el mismo concepto. Por ejemplo, la función `SUM` es la misma en Excel que en DAX.

En definitiva, podemos decir que el lenguaje DAX consta de muchas funciones. Las funciones son fórmulas predefinidas que realizan cálculos sobre valores específicos, llamados argumentos, en un orden particular. Cada función tiene una sintaxis específica que indica el orden esperado de los argumentos. Podemos encontrar todas las funciones disponibles para nosotros y su sintaxis en la [documentación de Microsoft](https://docs.microsoft.com/es-es/dax/dax-function-reference).

### Tipos de cálculos

En el menú superior, puede encontrar las opciones para crear un par de tipos diferentes de cálculos:

![DAX Power BI](/post/introduccion_power_bi/dax_power_bi.png)

- **Nuevas columnas:** Las columnas se pueden basar en otras columnas de cualquier tabla. Cualquier columna creada se calcula en la carga de datos o cuando se actualizan los datos. Por ejemplo, crearemos una nueva columna llamada `LoginID` extrayendo los dos primeros caracteres de una cadena de texto almacenado en la columna `FirstName`de la tabla `DimCustomer` y lo concatenaremos con el campo `LastName`de la misma tabla. Para ello, en la vista de datos podemos definir: `LoginID = LEFT(DimCustomer[FirstName], 2) & DimCustomer[LastName]`. 

- **Nuevas tablas**: Lo mismo ocurre con las tablas. Podemos crear una tabla en blanco o una copia de una tabla existente.

- **Nuevas medidas (nuevas medias o medidas rápidas)**: Las medidas son un poco diferentes. Nos permiten definir cálculos complejos que se utilizarán en sus datos. Se calculan a medida que interactúa y filtra en su informe. Por ejemplo, si filtramos por un año específico, nuestras medidas se basarán solo en ese año. A diferencia de las tablas y columnas calculadas, las medidas se calculan durante el tiempo de consulta en lugar de cuando se cargan los datos. Esto lo hace más eficiente porque el cálculo no se ejecuta cada vez que se accede a su tabla. En cambio, se calcula cuando se usa la medida. 

  Un medida que solemos utilizar a menudo es contar el numero de filas que tiene una tabla. Power BI tiene implementada la función `COUNT`. Este cálculo no lo podríamos hacer una una *Nueva columna* ya que necesitamos tener acceso a toda la tabla. El código  `Transaction Count = COUNT(FactInternalSales[SalesID])` proporciona el conteo de la columna `SalesID` en la tabla `FactInternalSales` donde cada fila representa una venta. 

Las medias y las columnas pueden llevar algo de confusión. En la siguiente tabla intento presentar las diferencias entre las dos: 

| Columnas                                          | Medias                                                       |
| ------------------------------------------------- | ------------------------------------------------------------ |
| Evalúa cada fila                                  | Agrega múltiples filas                                       |
| Agrega una nueva columna a una tabla existente    | Devuelve otro campo que se puede agregar a una visualización |
| Ejemplo: `Beneficio = Ventas - Coste - Impuestos` | Ejemplo: `Ventas medias = media de la columna ventas`        |

### Medidas y medidas rápidas

Una de las funciones de DAX más utilizadas es la función Calcular, que le permite combinar la agregación y el filtrado. Su estructura es la siguiente: `CALCULATE (Aggregation, filter, [filter]...)`. Para que la agregación se puede usar una función `SUM()`, `COUNT()`, `AVERAGE()`, etc. También, se necesitan uno o más filtros, por ejemplo, `ProductColor = RED` o `SalesLocation = "New York"`. 

Si queremos una medida calculada para la cantidad de ventas generada por la oficina de Nueva York. Podríamos usar la agregación de la suma para sumar todas las ventas y filtrarlas por ubicación de ventas de tal manera que `NYC Sales  = Calculate(SUM[Sales], SalesLocation = "New York")`

Otro aspecto importante que debe conocer al crear medidas es la herramienta **medidas rápidas**. Las medidas rápidas son útiles porque le permiten crear medidas complejas sin escribir ningún DAX. Lo único que necesitas para crearlas es arrastrar y soltar los campos necesarios. 

## Conclusión

En este breve tutorial hemos visto las diferentes vistas en Power BI, la creación de un modelo de datos para establecer relaciones entre sus tablas en la vista modelo y mostramos como crear un primer informe interactivo en la vista Informe. También hemos visto como se puede dar formato a las visualizaciones  para hacer más interpretables nuestras visualizaciones. Por último, hemos presentado el lenguaje de fórmulas de Microsoft, DAX y cómo usar los diferentes tipos de cálculos disponibles.  