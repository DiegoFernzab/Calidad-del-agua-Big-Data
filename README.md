# Análisis y Predicción de Calidad del Agua en India

## Descripción del proyecto

Este proyecto desarrolla un análisis de calidad del agua en India a partir de un conjunto de datos con variables fisicoquímicas y microbiológicas. El trabajo incluye limpieza de datos, tratamiento de valores nulos, cálculo del índice WQI, visualización geográfica por estado y entrenamiento de un modelo de Machine Learning con Keras para predecir el índice de calidad del agua.

## Objetivo

Construir un flujo de análisis que permita evaluar la calidad del agua mediante el índice WQI y aplicar técnicas de aprendizaje automático para estimar dicho índice a partir de variables originales como pH, oxígeno disuelto, conductividad, BOD, nitratos y coliformes fecales.

## Tecnologías utilizadas

- Python
- PySpark
- Pandas
- NumPy
- Matplotlib
- Seaborn
- GeoPandas
- Scikit-learn
- Keras / TensorFlow
- Jupyter Notebook

## Estructura general del proyecto

El cuaderno se organiza en las siguientes etapas:

1. **Carga de datos**  
   Se carga el archivo de calidad del agua y se realiza una primera revisión de columnas y registros.

2. **Limpieza y preparación**  
   Se reemplazan valores `"NA"` por valores nulos reales, se convierten variables numéricas a tipo `FloatType` y se imputan valores faltantes usando la mediana.

3. **Análisis exploratorio**  
   Se revisan estadísticas descriptivas, distribuciones, boxplots, valores extremos y correlaciones entre variables.

4. **Cálculo del WQI**  
   Se construyen subíndices de calidad para cada variable, se aplican ponderaciones y se calcula el índice WQI final.

5. **Clasificación de calidad**  
   El WQI se clasifica en categorías como `Muy_Baja`, `Baja`, `Moderada`, `Buena` y `Excelente`.

6. **Visualización geográfica**  
   Se calcula el WQI promedio por estado y se representa en un mapa de India para observar diferencias regionales.

7. **Modelo predictivo**  
   Se entrena un modelo Keras de regresión para predecir el valor del WQI usando las variables originales del agua.

## Variables utilizadas

Las variables principales consideradas en el análisis son:

- `TEMP`: temperatura del agua.
- `DO`: oxígeno disuelto.
- `pH`: nivel de acidez o alcalinidad.
- `CONDUCTIVITY`: conductividad eléctrica.
- `BOD`: demanda bioquímica de oxígeno.
- `NITRATE_N_NITRITE_N`: concentración de nitratos y nitritos.
- `FECAL_COLIFORM`: coliformes fecales.
- `WQI`: índice de calidad del agua calculado.
- `CALIDAD`: categoría asignada según el valor del WQI.

## Tratamiento de valores nulos

Durante la revisión inicial se identificaron valores faltantes representados como texto `"NA"`. Estos valores fueron convertidos a nulos reales y posteriormente imputados usando la mediana de cada variable numérica.

Se utilizó la mediana porque algunas variables, como `FECAL_COLIFORM` y `CONDUCTIVITY`, presentan valores extremos que podrían afectar el promedio.

## Cálculo del WQI

El índice WQI se calcula a partir de subíndices de calidad asociados a diferentes parámetros del agua. Cada subíndice se pondera según su importancia dentro del análisis.

En este proyecto, valores altos del WQI representan mejor calidad del agua, mientras que valores bajos indican condiciones menos favorables.

La clasificación usada fue:

| Rango WQI | Categoría |
|---|---|
| 0 - 25 | Muy_Baja |
| 25 - 50 | Baja |
| 50 - 75 | Moderada |
| 75 - 90 | Buena |
| 90 - 100 | Excelente |

## Modelo de regresión

Se entrenó un modelo de red neuronal usando Keras para predecir el valor numérico del WQI. Como variables de entrada se usaron los parámetros originales del agua, no los subíndices calculados, para evitar que el modelo aprendiera directamente la fórmula del WQI.

Las variables fueron normalizadas con `StandardScaler` antes del entrenamiento.

El modelo utilizado fue una red neuronal pequeña con:

- Capa de entrada con las variables originales.
- Una capa densa de 32 neuronas.
- Dropout para reducir sobreajuste.
- Una capa densa de 16 neuronas.
- Una salida lineal para predecir el WQI.

## Resultados del modelo

El modelo Keras de regresión fue evaluado con métricas de error sobre el conjunto de prueba.

Métricas obtenidas:

| Métrica | Resultado aproximado |
|---|---:|
| MAE | 7.5481 |
| MSE | 91.6616 |
| RMSE | 9.5740 |
| R² | 0.5243 |

El MAE indica que, en promedio, el modelo se equivoca alrededor de 7.5 puntos de WQI. El R² muestra que el modelo explica aproximadamente el 52% de la variabilidad del índice en los datos de prueba.

## Visualización geográfica

Para evitar representar un estado con una sola medición, se calculó el WQI promedio por estado. Esto permitió construir una visualización más representativa de la calidad promedio del agua en las regiones disponibles del dataset.

## Conclusiones

El proyecto permitió construir un flujo completo de análisis de calidad del agua, desde la limpieza de datos hasta la predicción del WQI mediante Machine Learning.

Se corrigieron problemas importantes relacionados con valores nulos, tipos de datos y clasificación del índice WQI. Además, el análisis exploratorio mostró la presencia de valores extremos en variables como coliformes fecales y conductividad, lo cual debe considerarse al interpretar los resultados.

El modelo de regresión logró una aproximación razonable al WQI, aunque todavía presenta margen de mejora. Para trabajos futuros, se recomienda complementar el análisis con modelos de clasificación para predecir directamente la categoría `CALIDAD` y comparar su desempeño con modelos clásicos como árboles de decisión o Random Forest.

## Referencias

- Scikit-learn. *train_test_split*.  
  https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html

- Scikit-learn. *StandardScaler*.  
  https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html

- TensorFlow. *Keras: API de alto nivel de TensorFlow*.  
  https://www.tensorflow.org/guide/keras?hl=es-419

- Documentación de Pandas.  
  https://pandas.pydata.org/docs/

- Documentación de PySpark.  
  https://spark.apache.org/docs/latest/api/python/

## Autor

Proyecto realizado como parte del análisis de calidad del agua usando técnicas de procesamiento de datos y aprendizaje automático.
