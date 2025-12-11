---
title: Estandarización de datos
author: Daniel Alcaide
date: 2021-12-14
tags:
- python
- estadística
categories:
- tutoriales
url: "/estandarizacion_de_datos"
showToc: false
TocOpen: false
draft: true

---
La **estandarización** de los datos es un paso común en el preprocesamiento. Ésta se puede definir como la acción de cambiar los datos para que estén centrados en el 0 y tengan una desviación estándar de 1. El objetivo es llevar las variables con diferentes unidades a una común. Muchas tareas de aprendizaje automático son sensibles a las magnitudes de los datos y se supone que la estandarización elimina esos factores. Por ejemplo, el método de *k-nearest neighbors* es sensible a las magnitudes de las variables, por lo que se deben estandarizar los datos. En cambio, los métodos basados en árboles (*tree-based methods*) no son sensibles a los diferentes rangos de las variables, por lo que la estandarización no es necesaria.

Otro paso común del preporocesamiento es la **normalización**. La normalización se refiere al proceso de mapear diferentes variables en el mismo rango [0, 1], y el escalado *min-max* se considera el algoritmo de normalización más común, aunque también existen otros algoritmos. 

La estadarización se preocupa más por la media y la desviación estándar. Ella intenta convertir (o aproximar) la distribución original en una distribución gaussiana. En el caso de que la distribución original sea realmente gaussiana, la normalización produce una distribución gaussiana estándar.

El proceso para estandarizar requiere calcular la desviación estándar y la media de los datos, los valores se restan con la media y luego  se divide por la desviación estándar. A continuación se muestra un ejemplo con la columna `Chol` del conjunto de datos de  [Heart Disease](https://archive.ics.uci.edu/ml/datasets/heart+disease):

```python
import pandas as pd
import numpy as np
 
# Read dataset
df = pd.read_csv('.../Heart.csv')
 
# Data standaridization for column 'Chol'
chol = df['Chol']
stdChol = np.std(chol)
meanChol = np.mean(chol)
chol2 = chol.apply(lambda x: (x-meanChol)/stdChol)
```
La estandarización de datos es irreversible y la información se perderá con la estandarización. Solo se recomienda hacerlo cuando no se requiera posteriormente información original, como magnitudes o desviación estándar original. En la siguiente ejemplo mostramos como realizar el mismo procedimento de utilizando el módulo de preprocesamiento de `scikit-learn`:

```python
from sklearn import preprocessing
 
# Select numeric variables
df2 = df[['Age', 'RestBP', 'Chol', 'MaxHR', 'Oldpeak', 'Ca']]
 
# Standardization
df3 = pd.DataFrame(preprocessing.scale(df2))
 
df3.mean(axis=0)
# ~ 0
df3.std(axis=0)
# ~ 1
```
Para terminar, veamos un ejemplo de normalización utilizando el algoritmo *min-max* (o `MinMaxScaler` en `sklearn`) para transformar cada variable en el rango [0, 1]. 

```python
df4 = pd.DataFrame(preprocessing.MinMaxScaler().fit_transform(df2))
 
df4.min(axis=0)
# 0
df4.max(axis=0)
# 1
```