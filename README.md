# Predicción de Popularidad de Canciones en Spotify

Proyecto para predecir la popularidad de canciones en Spotify a partir de sus características de audio.

## Estructura del proyecto

```
Spotify-Tracks-Dataset/
│
├── data/
│   ├── raw/              # dataset original sin modificar (dataset.csv)
│   └── processed/        # datos limpios y transformados
│
├── docs/
│   └── informe_tecnico.md  # informe técnico completo del proyecto
│
├── notebooks/
│   └── 01_analisis_spotify.ipynb
│
├── models/                # modelos entrenados (etapa futura)
│
├── images/                # gráficos exportados del EDA
│
├── README.md              # este archivo
└── requirements.txt       # librerías utilizadas
```

## Cómo ejecutar el proyecto

```bash
# Clonar el repositorio
git clone https://github.com/Starlitbloom/Spotify-Tracks-Dataset.git
cd Spotify-Tracks-Dataset

# Instalar dependencias
pip install -r requirements.txt

# Ejecutar el notebook
jupyter notebook notebooks/01_analisis_spotify.ipynb
```

## Dataset

[Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset) — Kaggle (autor: maharshipandya). Descargar y ubicar como `data/raw/dataset.csv`.

## Integrantes

- María Calfileo
- Stephanie Chamorro

**Asignatura:** Machine Learning (MLY1101)
**Docente:** Victor Trigo
**Institución:** Duoc UC — 2026