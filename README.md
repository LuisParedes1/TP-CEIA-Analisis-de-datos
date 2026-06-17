# TP-CEIA-Analisis-de-datos

Trabajo Final grupal para la materia Análisis de Datos - CEIA


## Integrantes

- Yoharlyn Alvarez: yoharlyn@gmail.com
- Sebastián Aragones: seraragones@gmail.com
- Luis Paredes: luisjosepr@gmail.com

## Enunciado

El enunciado completo se encuentra en [`enunciado/Analisis_de_datos_-_Trabajo_grupal_-_2B2026.pdf`](./enunciado/Analisis_de_datos_-_Trabajo_grupal_-_2B2026.pdf).


## Resumen

En el siguiente trabajo se realiza un análisis exploratorio, limpieza, preprocesamiento y reducción de dimensionalidad sobre el dataset [Full TMDB Movies Dataset 2024](https://www.kaggle.com/datasets/asaniczka/tmdb-movies-dataset-2023-930k-movies), que contiene metadatos asociados a 1.4 millones de películas.

El objetivo es construir un pipeline de análisis de datos orientado a predecir el éxito de una película, definido a partir de un success score bayesiano calculado con `vote_average` y `vote_count`.

$$WR = (v_i / (v_i + u)) · R_i  +  (u / (v_i + u)) \cdot C$$

donde 

- $R_i$ = vote_average de la película 
- $v_i$ = vote_count
- $C$ = media global de vote_average del dataset (el "prior"), 
- $u$ = umbral mínimo de votos para considerar el rating confiable (90%)


La idea es que si una película tiene muchos votos, $WR \approx R$ (confiamos en su rating); si tiene pocos, se la "tira" hacia la media global $C$

Por ultimo cada pelicula que se encuentre por encima del umbra (cuantil Q3 de la distribucion de `WR`) son consideradas exitosas y se asignan el label `success`

## Contenido del notebook

1. **EDA (Análisis Exploratorio):** identificación de valores nulos, distribuciones, correlaciones y visualizaciones clave.
2. **Limpieza y filtrado:** reducción a ~293k películas con votos válidos, fecha de lanzamiento y género.
3. **Encoding:** one-hot encoding de géneros, extracción de año y mes de lanzamiento.
4. **Selección de features:** ANOVA F-test, Chi-cuadrado e Información Mutua para evaluar el poder predictivo de cada variable.
5. **Reducción de dimensionalidad:** PCA a 2 componentes con biplot
