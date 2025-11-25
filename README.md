# Predicción de Popularidad de Canciones en Spotify mediante Machine Learning

Este proyecto forma parte del módulo de Machine Learning del bootcamp de Data & Inteligencia Artificial.  
El objetivo es construir un modelo de regresión para predecir la popularidad de una canción utilizando únicamente las características de audio provistas en el dataset de Spotify.

Se sigue un flujo estándar de Machine Learning: carga de datos, limpieza, selección de características, escalado, entrenamiento del modelo y evaluación.

---

## 1. Objetivos del proyecto

- Preparar un dataset real para Machine Learning.
- Aplicar técnicas básicas de limpieza de datos.
- Entrenar un modelo de regresión lineal para predecir popularidad.
- Evaluar métricas de rendimiento (MAE, RMSE, R²).
- Analizar la influencia de cada variable en el resultado.
- Generar conclusiones profesionales sobre la calidad del modelo.

---

## 2. Datos utilizados

El dataset proviene de Spotify y contiene información de más de 114,000 canciones.  
Incluye variables como:

- danceability  
- energy  
- loudness  
- speechiness  
- acousticness  
- instrumentalness  
- liveness  
- valence  
- tempo  
- duration_ms  
- popularity (variable objetivo)

El archivo utilizado es: 
data/spotify_tracks.csv


---

## 3. Preparación y limpieza de datos

Se realizaron los siguientes pasos:

1. Eliminación de columnas irrelevantes para el modelo:
   - track_id  
   - track_name  
   - artists  
   - album_name  

2. Eliminación de outliers extremos en duración:
   - Se mantuvieron canciones con menos de 600,000 ms (10 minutos).

3. Eliminación de duplicados.

4. Selección de variables numéricas relevantes para el modelo.

Estas transformaciones generaron el dataset final usado para entrenar el modelo.

---

## 4. Selección de características

Las variables predictoras seleccionadas fueron:

- danceability  
- energy  
- loudness  
- speechiness  
- acousticness  
- instrumentalness  
- liveness  
- valence  
- tempo  
- duration_ms  

Variable objetivo (target):

- popularity

---

## 5. División Train/Test y escalado

Se utilizó un 80% de los datos para entrenamiento y 20% para prueba.

Las variables predictoras se escalaron utilizando StandardScaler para mejorar el rendimiento del modelo de regresión lineal.

---

## 6. Entrenamiento del modelo

Se utilizó un modelo de **Regresión Lineal** como aproximación inicial y didáctica al problema.

---

## 7. Resultados y métricas

Los valores obtenidos fueron:

- MAE: 18.47  
- RMSE: 22.12  
- R²: 0.0228  

Interpretación:

- El error promedio del modelo es de aproximadamente 18 puntos de popularidad.
- El modelo solo explica el 2.28% de la variación en la popularidad.
- El rendimiento es bajo y refleja que las características de audio no son suficientes para predecir popularidad.

---

## 8. Importancia de las variables

Coeficientes del modelo (ordenados por influencia):

| Feature            | Coeficiente |
|-------------------|-------------|
| danceability      | 1.59        |
| loudness          | 0.59        |
| tempo             | 0.46        |
| liveness          | 0.30        |
| duration_ms       | 0.05        |
| acousticness      | -0.39       |
| energy            | -0.75       |
| speechiness       | -1.29       |
| instrumentalness  | -2.44       |
| valence           | -2.48       |

Conclusiones:
- Las variables con impacto positivo (danceability, loudness, tempo) tienen una influencia baja.
- Variables como instrumentalness, valence y speechiness tienen influencia negativa.
- Ninguna variable por sí sola explica fuertemente la popularidad.
- La información de audio tiene un poder predictivo muy limitado.

---

## 9. Conclusión general

Los resultados del modelo confirman que la popularidad de una canción en Spotify **no puede predecirse adecuadamente usando solo características de audio**.

La popularidad depende de factores externos como:
- marketing y promoción,
- presencia en playlists editoriales,
- viralidad en redes sociales,
- fama del artista,
- tendencias del mercado.

El modelo entrenado sirve como demostración técnica del proceso de Machine Learning, pero no logra un desempeño adecuado para predicciones reales.

---

## 10. Limitaciones del modelo

- Las características de audio no capturan elementos importantes como letras, género o contexto social.
- La variable popularidad cambia con el tiempo y no es estática.
- Falta información externa relevante (seguidores, playlists, tendencias, lanzamiento).
- Presencia de ruido y outliers naturales en datos musicales.
- La regresión lineal es un modelo demasiado simple para patrones complejos.

---

## 11. Próximos pasos

- Probar modelos más complejos (Random Forest, XGBoost).
- Incluir variables externas del artista o historial del track.
- Probar modelos de clasificación (popularidad alta vs baja).
- Implementar tuning de hiperparámetros.
- Analizar géneros por separado para mejorar el ajuste.

## 12. Modelo Random Forest

Además de la regresión lineal, se entrenó un modelo **Random Forest Regressor** con el objetivo de mejorar la capacidad predictiva utilizando un algoritmo más robusto y no lineal. Este tipo de modelo puede capturar relaciones más complejas entre las características de audio y la popularidad, algo que la regresión lineal no logra.

### Configuración del modelo

Se utilizó la siguiente configuración:

- n_estimators = 200  
- random_state = 42  
- n_jobs = -1 (uso de todos los núcleos disponibles)  
- max_depth = None  
- min_samples_leaf = 1  

El modelo se entrenó con:

```python
rf = RandomForestRegressor(
    n_estimators=200,
    random_state=42,
    n_jobs=-1,
    max_depth=None,
    min_samples_leaf=1
)

rf.fit(X_train, y_train)
13. Resultados del modelo Random Forest

Las métricas obtenidas fueron:

MAE: 10.59

RMSE: 14.98

R²: 0.5513

Interpretación de resultados

El MAE disminuyó de 18.47 (Regresión Lineal) a 10.59.

El R² aumentó de 0.0228 a 0.5513, mostrando un incremento significativo en la capacidad predictiva.

El Random Forest explica aproximadamente el 55% de la variación de la popularidad, un resultado muy superior al modelo lineal.

Esto confirma que existen relaciones no lineales entre las características de audio y la popularidad, mejor capturadas por modelos basados en árboles.

14. Importancia de variables

El modelo Random Forest permitió obtener la importancia relativa de cada feature:

Feature	Importancia
acousticness	0.1119
duration_ms	0.1079
danceability	0.1066
tempo	0.1066
valence	0.1046
speechiness	0.1028
loudness	0.0995
energy	0.0953
liveness	0.0912
instrumentalness	0.0738
Interpretación

Las variables con mayor importancia fueron: acousticness, duration_ms, danceability y tempo.

A diferencia de la regresión lineal, el modelo Random Forest muestra una relevancia más equilibrada entre las características.

La información de audio sí contribuye al modelo, pero de manera compleja y no lineal.

15. Gráfica de importancia de variables

Se generó también una gráfica que muestra visualmente la importancia de cada variable dentro del Random Forest.

Esta gráfica se encuentra en:

/images/random_forest_feature_importance.png

16. Conclusión del modelo Random Forest

El modelo Random Forest ofrece una mejora significativa respecto a la regresión lineal, mostrando que:

La relación entre características de audio y popularidad no es lineal.

Un modelo más complejo puede capturar mejor los patrones del dataset.

El rendimiento obtenido (R² = 0.55) es aceptable considerando la naturaleza de los datos y sus limitaciones.

Aun así, la popularidad sigue estando influenciada por factores externos que este dataset no incluye.
