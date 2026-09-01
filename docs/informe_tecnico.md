# Informe Técnico: Predicción de Popularidad de Canciones en Spotify

**Asignatura:** Machine Learning (MLY1101)
**Docente:** Victor Trigo
**Institución:** Duoc UC
**Integrantes:** María Calfileo, Stephanie Chamorro
**Año:** 2026

---

## 1. Descripción del problema de negocio

Las plataformas de streaming y discográficas necesitan decidir en qué canciones invertir, qué temas incluir en playlists destacadas y qué artistas priorizar en su promoción. Tomar estas decisiones a la ligera implica un alto riesgo financiero y de oportunidad.

Con este proyecto se busca predecir la popularidad de una canción a partir de sus características de audio, permitiendo a discográficas o plataformas de streaming tomar decisiones de promoción e inversión basadas en datos, en lugar de intuición.

## 2. Objetivos del proyecto

**Objetivo general:**
Desarrollar un modelo de Machine Learning capaz de predecir el nivel de popularidad de una canción a partir de sus atributos de audio.

**Objetivos específicos:**
- Realizar un análisis exploratorio de los datos para identificar patrones entre características de audio y popularidad.
- Preparar y transformar los datos para dejarlos listos para el proceso de modelamiento.
- Evaluar posibles sesgos y consideraciones éticas asociadas al uso de este dataset.

## 3. Definición de KPIs

| KPI | Descripción | Resultado en este proyecto |
|---|---|---|
| Correlación de features de audio con popularidad | Identificar qué variables tienen mayor relación lineal con la popularidad | Máxima correlación encontrada: -0.09 (instrumentalness) — ninguna variable individual es un buen predictor lineal |
| % de canciones con popularidad = 0 | Medir qué proporción del catálogo no logra tracción en la plataforma | 13.95% del dataset |
| Cobertura de datos limpios | % de filas utilizables tras la limpieza | 99.6% (113.549 de 114.000 filas originales) |
| Dimensionalidad tras preparación | N° de variables predictoras finales tras codificación | 127 columnas (desde 16 originales) |

## 4. Descripción de las fuentes de datos

**Dataset:** [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
**Fuente:** Kaggle (autor: maharshipandya)
**Formato:** CSV (`dataset.csv`)
**Ubicación en el proyecto:** `data/raw/`

**Dimensiones:** 114.000 filas × 21 columnas originales (113.549 filas tras la limpieza de duplicados y del registro corrupto).

**Principales columnas:**
- `popularity`: variable objetivo (escala 0-100).
- `track_genre`: 114 géneros musicales distintos.
- Características de audio: `danceability`, `energy`, `loudness`, `speechiness`, `acousticness`, `instrumentalness`, `liveness`, `valence`, `tempo`, `key`, `mode`, `time_signature`.
- Identificadores y metadata: `track_id`, `artists`, `album_name`, `track_name`, `duration_ms`, `explicit`.

## 5. Preparación y análisis exploratorio de los datos (EDA)

### 5.1 Calidad de los datos

- **Valores nulos:** se detectó un único registro corrupto (índice 65900), sin metadata (`artists`, `album_name`, `track_name` nulos) y con `duration_ms = 0`. Fue eliminado. Tras esto, el dataset no presenta valores nulos.
- **Duplicados exactos:** al eliminar la columna `Unnamed: 0` (índice residual), se revelaron 450 filas exactamente duplicadas, las cuales fueron eliminadas.
- **Duplicados por `track_id` (24.259 casos):** corresponden a canciones catalogadas legítimamente en múltiples géneros (hasta 9 géneros distintos por canción). No se eliminaron, ya que representan información válida.
- **Columnas eliminadas:** `Unnamed: 0`, por no aportar valor analítico.

### 5.2 Análisis exploratorio

- **Distribución de la variable objetivo:** `popularity` presenta una distribución multimodal (no normal), con una fuerte concentración en 0 (13.95% de las canciones). Estos casos se concentran en géneros tradicionales o de nicho (`jazz`, `iranian`, `soul`, `country`, `latin`, `romance`), y no en géneros masivos.
- **Correlaciones con popularidad:** ninguna variable de audio individual muestra correlación relevante con `popularity` (todas por debajo de 0.10 en valor absoluto). Esto sugiere que la popularidad depende de factores no capturados directamente en las características sonoras (marketing, algoritmo de recomendación, contexto del artista).
- **Multicolinealidad entre variables de audio:** se detectó correlación fuerte entre `energy` y `loudness` (0.76), y relación inversa entre ambas y `acousticness` (-0.73 y -0.59 respectivamente).
- **Popularidad por género:** `pop-film` y `k-pop` lideran el promedio de popularidad (~59 y ~57), seguidos de géneros asociados a estados de ánimo como `chill` y `sad`.
- **Outliers detectados:** valores de `tempo` y `time_signature` en 0 (163 y 157 casos, concentrados en el género `sleep`/`ambient`), duración máxima de ~87 minutos (un mix de DJ del género `minimal-techno`, caso legítimo), duración mínima de ~8.6 segundos (caso sospechoso, posible clip mal catalogado), y 90 casos de `loudness` positivo (masterización agresiva, fenómeno real de la industria). La mayoría de estos valores corresponden a características genuinas del dominio musical y no a errores de captura.

### 5.3 Preparación de datos para modelamiento

- **Imputación:** los 157 casos de `tempo = 0` fueron reemplazados por la mediana de tempo de su propio género musical.
- **Codificación de variables categóricas:** `track_genre` (114 categorías) mediante one-hot encoding, generando 113 columnas nuevas.
- **Exclusión de variables:** se descartaron `track_id`, `track_name`, `artists` y `album_name` por ser identificadores de alta cardinalidad sin valor predictivo directo.
- **Escalamiento:** estandarización (`StandardScaler`) sobre las 9 variables de audio, ajustada únicamente con datos de entrenamiento para evitar fuga de datos (*data leakage*).
- **División train/test:** 80% entrenamiento (90.839 filas) / 20% prueba (22.710 filas), `random_state=42`.
- **Resultado final:** 127 columnas predictoras (desde 16 originales), producto principalmente del one-hot encoding de género.

## 6. Metodología utilizada (CRISP-DM)

Este proyecto sigue la metodología **CRISP-DM** (Cross Industry Standard Process for Data Mining):

1. **Comprensión del negocio:** definición del problema, objetivos y KPIs (secciones 1-3).
2. **Comprensión de los datos:** exploración inicial del dataset, calidad y estructura (sección 5.1).
3. **Preparación de los datos:** limpieza, transformación y codificación de variables (sección 5.3).
4. **Modelamiento:** fuera del alcance de esta evaluación parcial; queda como trabajo futuro (ver recomendaciones).
5. **Evaluación:** no aplica en esta etapa, al no existir un modelo entrenado aún.
6. **Despliegue:** no aplica en esta evaluación; se describen recomendaciones de implementación responsable en la sección de consideraciones éticas.

## 7. Consideraciones éticas y de sesgos

- **Sesgo de representación (confirmado con evidencia):** el dataset está artificialmente balanceado por género — 114 géneros con una desviación estándar de solo 11.84 canciones entre ellos (rango 904-1.000). Esto no refleja la distribución real de géneros consumidos en Spotify, donde géneros mainstream concentran mucho mayor volumen de streams y catálogo.
- **Sesgo cultural (confirmado con evidencia):** el 13.95% de canciones con popularidad = 0 se concentra en géneros culturalmente específicos (`jazz`, `iranian`, `soul`, `latin`, `romance`), mientras géneros como `pop-film` y `k-pop` dominan el promedio de popularidad. Esto podría reflejar sesgos del propio algoritmo de recomendación de Spotify —que favorece ciertos mercados y estéticas— más que diferencias objetivas de calidad musical.
- **Riesgo de retroalimentación (feedback loop):** un modelo entrenado con estos datos podría reforzar el sesgo existente: al predecir menor popularidad para géneros ya marginados, se les asignaría menos promoción, reduciendo aún más su alcance real y confirmando la predicción de forma artificial.
- **Impacto emocional y bienestar del oyente:** géneros asociados a estados de ánimo (`chill`, `sad`) figuran entre los de mayor popularidad promedio. Esto abre una pregunta ética relevante: ¿es responsable optimizar un algoritmo para maximizar el consumo de contenido asociado a estados emocionales negativos si esto incrementa métricas de negocio pero no necesariamente el bienestar del oyente?
- **Privacidad:** el dataset no contiene datos personales de usuarios (sin historiales de escucha, ubicación o identidad de oyentes), por lo que el riesgo de privacidad individual es bajo. La responsabilidad ética se concentra en el impacto sobre artistas y géneros musicales, no sobre usuarios finales.
- **Recomendaciones de mitigación:** (a) no usar la predicción de popularidad como único criterio de inversión en promoción, complementándola con criterios de diversidad cultural; (b) monitorear si el modelo perpetúa sistemáticamente bajas predicciones para ciertos géneros; (c) evitar entrenar un modelo de producción exclusivamente con este dataset balanceado artificialmente, dado que no representa la distribución genuina del catálogo real de la plataforma; (d) incorporar salvaguardas que eviten la sobreexposición sostenida a contenido de valencia emocional negativa en un mismo oyente.

## 8. Conclusiones y próximos pasos

El análisis exploratorio permitió comprender en profundidad la estructura, calidad y particularidades del dataset de Spotify. El hallazgo más relevante es que **la popularidad de una canción no depende linealmente de sus características de audio individuales**, lo que sugiere que un futuro modelo debería considerar algoritmos no lineales (ej. Random Forest, Gradient Boosting) y, muy probablemente, incorporar el género musical como variable predictora relevante — siempre teniendo en cuenta las salvaguardas éticas identificadas para evitar perpetuar sesgos de representación existentes en la plataforma.

Como próximos pasos, este proyecto sienta las bases (datos limpios, preparados y documentados) para una futura etapa de modelamiento y evaluación de algoritmos predictivos.
