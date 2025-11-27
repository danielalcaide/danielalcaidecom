---
title: "Análisis de riesgo en Social Trading con arquitectura Lakehouse"
author: "Daniel Alcaide"
date: '2025-11-27'
tags: ["python", "databricks", "finanzas"]
categories: ["proyectos"]
url: /social-trading-risk-analytics
---

En las plataformas de *social trading* como eToro, los inversores pueden copiar las estrategias de traders experimentados. Sin embargo, la mayoría de usuarios se fijan únicamente en la rentabilidad, ignorando el riesgo asociado. Este proyecto aborda precisamente ese problema.

<!--more-->

## El problema

Las plataformas de *social trading* destacan a los traders con mayores retornos, pero **altos rendimientos no siempre implican bajo riesgo**. Dos traders con un 30% de rentabilidad anual pueden tener perfiles de riesgo completamente diferentes:

- **Trader A:** Ganancias consistentes, ratios Sharpe 2.0 y Sortino 2.5
- **Trader B:** Año volátil, ratios Sharpe 0.5 y Sortino 0.4

La experiencia del inversor será radicalmente distinta: mientras que con el Trader A se mantiene la calma durante las fluctuaciones, con el Trader B existe el riesgo de vender en pánico ante una caída del 60%.

## La solución

He desarrollado una plataforma de análisis que proporciona:

- **Métricas ajustadas por riesgo** (Sharpe, Sortino, Calmar) para una evaluación completa
- **Análisis de diversificación** de carteras (sectores, bolsas, países)
- **Identificación de traders de élite** basada en criterios de rendimiento sostenible
- **Insights basados en datos** que sustituyen decisiones emocionales

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

### Métricas financieras clave

El análisis se centra en dos métricas principales:

**Ratio de Sortino** (métrica primaria)
- Penaliza solo la volatilidad a la baja (pérdidas)
- Ignora la volatilidad al alza (beneficiosa para inversores)
- Visión más realista del riesgo real

**Ratio de Calmar** (métrica secundaria)
- Revela resiliencia ante el peor escenario posible
- Identifica traders que sobreviven a las caídas del mercado
- Muestra sostenibilidad psicológica

## Resultados

El análisis de más de 1.000 traders reveló hallazgos interesantes:

1. **Solo el 15-20% de los traders con mayores retornos cumple los criterios de élite** (Sortino > 7, Calmar > 7), lo que indica que la mayoría asume riesgos excesivos

2. **El ratio Sortino es consistentemente 1.3-1.8x superior al Sharpe** para traders de élite, demostrando retornos asimétricos (ganancias ocasionales grandes, pérdidas mínimas)

3. **Los traders con Calmar < 0.3 tienen un 60% más de rotación**, ya que las caídas profundas provocan ventas por pánico

4. **Los traders de élite presentan un beta promedio de 0.7**, indicando estrategias market-neutral o posicionamiento defensivo

## Stack tecnológico

- **Databricks** (DBR 13.x): Plataforma de analítica unificada
- **Apache Spark** (3.4+): Procesamiento distribuido de datos
- **Delta Lake** (2.0+): Almacenamiento confiable en data lake
- **Python** (3.9+): Lenguaje principal de desarrollo
- **BeautifulSoup4**: Parsing de HTML
- **PySpark & Pandas**: Análisis de datos

## Próximos pasos

Las siguientes mejoras están planificadas:

- **Modelo ML** para predecir degradación del rendimiento de traders
- **Dashboard interactivo** en Streamlit para comparación de traders
- **API RESTful** para acceso programático a rankings
- **Sistema de alertas** en tiempo real cuando métricas crucen umbrales
- **Framework de backtesting** para estrategias de copy trading

El código completo está disponible en mi [repositorio de GitHub](https://github.com/danielalcaide/social-trading-risk-analytics).