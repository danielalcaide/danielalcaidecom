---
title: "Introducción a Power BI"
author: "Daniel Alcaide"
date: '2021-04-28'
tags: ["power bi"]
categories: ["tutoriales"]
url: /introduccion_powerbi
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

