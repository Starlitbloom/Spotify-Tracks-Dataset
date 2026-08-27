# Predicción de Popularidad de Canciones en Spotify
Proyecto para predecir la popularidad de canciones en Spotify a partir del audio.

## 1. Descripción del problema de negocio
Las plataformas de streaming y discográficas necesitan decidir en qué canciones invertir, qué temas incluir en playlists y que artistas deben priorizar. Tomar estas decisiones a la ligera implica un alto riesgo financiero y de oportunidades.

Con este proyecto se busca predecir la popularidad de una canción a partir de sus características de audio, permitiendo a las discográficas o plataformas de streaming tomar decisiones de promoción e inversión basadas en los datos.

## 2. Objetivos del proyecto
**Objetivo general:**
Desarrollar un modelo de Machine Learning que sea capaz de predecir el nivel de popularidad de una canción a partir de los atributos de audio que tenga.

**Objetivos específicos:**
- Realizar un análisis exploratorio de los datos para identificar patrones entre características de audio y popularidad.
- Preparar y transformar los datos para dejarlos listos para el modelamiento.
- Evaluar posibles sesgos y consideraciones éticas asociadas al uso de este dataset.

## 3. Descripción de las fuentes de datos

**Dataset:** [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
**Fuente:** Kaggle (autor: maharshipandya)
**Formato:** CSV
**Ubicación en el proyecto:** `data/raw/`

> _Completar tras la primera exploración:_
- N° de filas y columnas:
- Principales columnas (features de audio, género, artista, popularidad, etc.):

## 5. Preparación y análisis exploratorio de los datos (EDA)

### 5.1 Calidad de los datos
- Valores nulos encontrados y tratamiento aplicado:
- Duplicados encontrados y tratamiento aplicado:
- Columnas irrelevantes eliminadas (y por qué):

### 5.2 Análisis exploratorio
- Distribución de la variable popularidad:
- Correlaciones relevantes entre features de audio y popularidad:
- Diferencias de popularidad por género musical:
- Outliers detectados y decisión tomada:

### 5.3 Preparación de datos para modelamiento
- Codificación de variables categóricas:
- Escalamiento/normalización aplicado:
- División train/test (proporción utilizada):

## 7. Consideraciones éticas y de sesgos
- **Sesgo de representación:** ¿el dataset sobre-representa ciertos géneros, idiomas o mercados musicales?
- **Riesgo de retroalimentación:** un modelo que prioriza patrones "populares" podría homogeneizar la música promocionada y perjudicar a artistas emergentes o de nicho.
- **Sesgo cultural:** la "popularidad" en Spotify puede reflejar sesgos de mercados específicos (ej: EE.UU./Europa) y no representar gustos globales.
- **Privacidad:** este dataset no contiene datos personales de usuarios, por lo que el riesgo de privacidad es bajo, pero sí existe responsabilidad en cómo se usan las predicciones (ej: excluir sistemáticamente ciertos géneros de la promoción).

## 8. Estructura del proyecto
Spotify-Tracks-Dataset/
│
├── data/
│   ├── raw/              # dataset original sin modificar
│   └── processed/        # datos limpios y transformados
│
├── notebooks/
│   └── 01_analisis_spotify.ipynb
│
├── models/                # modelos entrenados (mas a adelante)
│
├── images/                # gráficos exportados del EDA
│
├── README.md              # este archivo
└── requirements.txt       # librerías que se van a utilizar
```


## 9. Cómo ejecutar el proyecto

```bash
# Clonar el repositorio
git clone https://github.com/TU-USUARIO/Spotify-Tracks-Dataset.git
cd Spotify-Tracks-Dataset

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar el notebook
jupyter notebook notebooks/01_analisis_spotify.ipynb
```

---

## 10. Integrantes
- María Calfileo
- Stephanie Chamorro

**Asignatura:** Machine Learning
**Docente:** Victor Trigo
