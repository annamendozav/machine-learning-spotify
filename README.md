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


