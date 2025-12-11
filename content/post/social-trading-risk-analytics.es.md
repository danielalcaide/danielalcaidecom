---
title: "De 1.500 traders a 6 de élite: Sistema de análisis de riesgo financiero con Databricks y Python"
author: "Daniel Alcaide"
date: '2025-12-11'
tags: ["python", "databricks", "finanzas"]
categories: ["proyectos"]
url: social-trading-risk-analytics
---

En las plataformas de *social trading* como eToro, los inversores pueden copiar las estrategias de traders experimentados. Sin embargo, la mayoría de usuarios se fijan únicamente en la rentabilidad, ignorando el riesgo asociado. Este proyecto aborda precisamente ese problema.

<!--more-->

## El problema

Las plataformas de *social trading* destacan a los traders con mayores retornos, pero **altos rendimientos no siempre implican bajo riesgo**. Para entender por qué, necesitamos hablar de métricas ajustadas por riesgo:

**Ratio de Sharpe:** Mide el retorno extra obtenido por unidad de volatilidad total. Un Sharpe de 2.0 significa que por cada punto de riesgo asumido, se obtienen 2 puntos de retorno. Valores superiores a 1.0 se consideran buenos.

**Ratio de Sortino:** Similar al Sharpe, pero solo penaliza la volatilidad negativa (pérdidas), ignorando las fluctuaciones al alza. Es más realista para inversores, ya que las subidas no son "riesgo". Un Sortino de 2.0+ es excelente.

**Ratio de Calmar:** Compara el retorno anualizado con la máxima caída histórica (drawdown). Un Calmar de 1.0 significa que si el trader ganó 30% anual pero tuvo una caída máxima del 30%, su ratio es 1.0. Valores superiores a 3.0 indican gran resiliencia.

**Beta:** Mide la sensibilidad de un trader respecto al mercado. En este proyecto usamos el índice S&P 500. Un beta de 1.0 significa que se mueve exactamente igual que el S&P 500, 1.5 indica 50% más de volatilidad que el índice, y 0.5 indica la mitad. Valores bajos (< 1.0) sugieren estrategias defensivas o market-neutral.

### El mismo retorno, riesgos opuestos

Con estos conceptos claros, veamos dos traders con 30% de rentabilidad anual:

- **Trader A:** Ganancias consistentes, Sharpe 2.0 y Sortino 2.5 (bajo riesgo)
- **Trader B:** Año volátil, Sharpe 0.5 y Sortino 0.4 (alto riesgo)

La experiencia del inversor será radicalmente distinta: mientras que con el Trader A se mantiene la calma durante fluctuaciones moderadas, con el Trader B existe el riesgo de vender en pánico ante una caída del 60%.

## La solución

He desarrollado una plataforma de análisis que proporciona:

- **Métricas ajustadas por riesgo** (Sharpe, Sortino, Calmar) para una evaluación completa
- **Análisis de diversificación** de carteras (sectores, bolsas, países)
- **Identificación de traders de élite** basada en criterios de rendimiento sostenible
- **Insights basados en datos** que sustituyen decisiones emocionales

## Metodología y dataset

El análisis se realizó sobre un dataset recopilado durante 6 meses. Los datos se van actualizando diariamente en pequeños subcojuntos priorizando los que hace más tiempo que no se han actualizado:

**Características del dataset:**
- **1.500 traders analizados** con historial completo de métricas
- **Período de recolección:** 29 de junio - 11 de diciembre de 2025
- **21 variables por trader** incluyendo métricas de riesgo, composición de cartera y datos de mercado.

![Figura 1](/post/social-trading-risk-analytics/data-collection-timeline.png)

*Figura 1: Timeline de recolección de datos mostrando el número de traders actualizados por última vez*

### Distribución de rentabilidades

El análisis de rentabilidades anualizadas revela una distribución interesante:

**Estadísticas clave:**
- **Media:** 15.60% anual
- **Mediana:** 15.09% anual
- **Desviación estándar:** 21.37%
- **Percentil 75:** 23.80% anual
- **Percentil 90:** 34.80% anual


![Figura 2](/post/social-trading-risk-analytics/distribution-of-annualized-returns.png)


*Figura 2: Distribución de rentabilidades anualizadas. La mayoría de traders se concentra entre 0-25%, con una cola larga hacia rentabilidades extraordinarias*

La distribución muestra una concentración significativa alrededor de la media, con aproximadamente 800 traders (53%) agrupados en el rango de 0-25% de rentabilidad anual. Sin embargo, la cola derecha extendida revela traders excepcionales con retornos superiores al 100% anual, aunque estos casos requieren un análisis especialmente cuidadoso del riesgo asumido.

### Arquitectura técnica

El proyecto implementa una arquitectura Medallion (Bronze → Silver → Gold) en Databricks:

**Bronze (Datos crudos):**
- Respuestas HTML inmutables de perfiles de traders
- Patrón append-only que permite reprocesamiento completo
- Manejo de códigos de estado HTTP para debugging

**Silver (Datos curados):**
- Métricas de riesgo parseadas y validadas
- Composición de carteras en formato normalizado
- Calidad de datos garantizada mediante validaciones

**Gold (Analítica):**
- Traders de élite (Sortino > 7 Y Calmar > 7)
- Top performers por rentabilidad anualizada
- Datos listos para sistemas de recomendación

## Análisis del top 25% de performers

Examinando el cuartil superior de traders (375 de los 1.500 analizados), encontramos perfiles de riesgo significativamente diferentes a la media:

**Métricas de riesgo del top 25%:**

| Métrica | Media | Mediana | Q1 | Q3 | Máximo |
|---------|-------|---------|----|----|--------|
| **Sharpe Ratio** | 1.05 | 0.94 | 0.77 | 1.21 | 3.80 |
| **Sortino Ratio** | 2.43 | 2.00 | 1.58 | 2.77 | 10.00 |
| **Calmar Ratio** | 1.77 | 1.02 | 0.61 | 2.23 | 10.00 |
| **Beta** | 1.21 | 1.12 | 0.88 | 1.46 | 3.30 |

### Visualización de riesgo-retorno

![Figura 3](/post/social-trading-risk-analytics/risk-adjusted-performance-sortino-vs-calmar-ratio.png)

*Figura 3: Scatter plot de Sortino vs Calmar para el top 25% de performers. Los traders de élite (ambas métricas > 7) aparecen en el cuadrante superior derecho*

El gráfico revela varios insights importantes:

1. **Mayoría subestimada:** Solo 6 traders (1.6% del top 25%) cumplen ambos criterios de élite (Sortino > 7 Y Calmar > 7)

2. **Distribución asimétrica:** La mayoría de traders se agrupa en el rango Sortino 2-4 y Calmar 0.5-3, indicando riesgo moderado-alto

3. **Outliers excepcionales:** Traders como `ferdisavage` (Sortino 10, Calmar 10, Retorno 297.89%) representan casos estadísticamente raros pero reales

## Los traders de élite

De los 1.500 traders analizados, solo 6 cumplen los criterios más estrictos de élite (Sortino > 7 Y Calmar > 7):

| Trader | Retorno Anual | Sharpe | Sortino | Calmar | Beta | Score |
|--------|---------------|--------|---------|--------|------|-------|
| **ferdisavage** | 297.89% | 3.75 | 10.00 | 10.00 | 0.92 | 10.00 |
| **Kevin_Pando** | 82.07% | 3.15 | 10.00 | 10.00 | 0.57 | 10.00 |
| **Eugene_sofoklaio** | 134.46% | 3.80 | 10.00 | 10.00 | 0.60 | 10.00 |
| **PelosiTracker** | 132.91% | 2.49 | 8.37 | 10.00 | 0.43 | 9.18 |
| **edu-inversor** | 46.32% | 1.00 | 7.82 | 8.67 | 0.81 | 8.25 |
| **CrijnWijers** | 52.14% | 2.41 | 8.68 | 7.70 | 0.88 | 8.19 |

**Características comunes de los traders de élite:**
- **Betas bajas/medias:** Rango 0.43-0.92, muy por debajo del 1.21 del top 25%
- **Retornos asimétricos:** Sortino consistentemente > 2x el Sharpe ratio
- **Resiliencia excepcional:** Calmar ratios que demuestran recuperación ante drawdowns
- **Diversidad de enfoques:** Retornos desde 46% hasta 298%, todos con riesgo controlado

## Resultados y hallazgos clave

El análisis de más de 1.500 traders reveló hallazgos interesantes:

1. **Solo el 0.4% de todos los traders cumple los criterios de élite** (6 de 1.500), y solo el 1.6% del top 25% de performers, lo que indica que la mayoría asume riesgos excesivos incluso entre los mejores

2. **El ratio Sortino es consistentemente 2.3x superior al Sharpe** (media 2.43 vs 1.05) para el top 25%, demostrando retornos asimétricos (ganancias ocasionales grandes, pérdidas mínimas)

3. **Los traders con Calmar < 1.0 representan el 50% del top 25%**, sugiriendo que incluso traders exitosos experimentan drawdowns significativos que podrían provocar ventas por pánico

4. **Los traders de élite presentan un beta promedio de 0.70**, significativamente inferior al 1.21 del top 25%, indicando estrategias market-neutral o posicionamiento defensivo

5. **La mediana del top 25% (Sortino 2.0, Calmar 1.02) está muy por debajo del umbral de élite (7.0)**, revelando una brecha enorme entre traders buenos y excepcionales

## Stack tecnológico

- **Databricks** (DBR 13.x): Plataforma de analítica unificada
- **Apache Spark** (3.4+): Procesamiento distribuido de datos
- **Delta Lake** (2.0+): Almacenamiento confiable en data lake
- **Python** (3.9+): Lenguaje principal de desarrollo
- **BeautifulSoup4**: Parsing de HTML
- **PySpark & Pandas**: Análisis de datos
- **Matplotlib & Seaborn**: Visualizaciones estadísticas

## Próximos pasos

Las siguientes mejoras están planificadas:

- **Modelo ML** para predecir degradación del rendimiento de traders basado en patrones históricos
- **Dashboard interactivo** en Streamlit para comparación dinámica de traders
- **API RESTful** para acceso programático a rankings y métricas en tiempo real
- **Sistema de alertas** que notifique cuando métricas crucen umbrales críticos
- **Framework de backtesting** para validar estrategias de copy trading antes de inversión real
- **Análisis de correlación** entre traders para optimización de carteras multi-trader

## Conclusiones

Este proyecto demuestra que **el rendimiento ajustado por riesgo es fundamentalmente diferente al rendimiento absoluto**. Mientras que las plataformas de social trading destacan a traders con retornos del 50-300% anual, solo una fracción minúscula (0.4%) combina estos retornos con perfiles de riesgo sostenibles.

Para inversores, la lección es clara: antes de copiar a un trader, analiza no solo cuánto gana, sino **cómo lo gana**. Un trader con 40% anual y Sortino 8.0 probablemente proporcionará mejor experiencia (y retorno compuesto a largo plazo) que uno con 100% anual y Sortino 0.5.

El código completo está disponible en mi [repositorio de GitHub](https://github.com/danielalcaide/social-trading-risk-analytics-platform).
