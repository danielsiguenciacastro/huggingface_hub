---
language: en
tags:
- breast-cancer
- classification
- random-forest
- medical-ai
- sklearn
datasets:
- breast-cancer-wisconsin
---

# Model Card for CANCER_DE_MAMA

**CANCER_DE_MAMA** es un modelo de machine learning basado en Random Forest diseñado para clasificar tumores de mama como benignos o malignos utilizando características médicas extraídas de imágenes de biopsias.

## Model Details

### Model Description

Este modelo utiliza un clasificador Random Forest entrenado con el dataset de cáncer de mama de scikit-learn para predecir si un tumor es benigno o maligno basándose en 30 características diferentes extraídas de imágenes digitalizadas de muestras de tumores.

- **Developed by:** Daniel Siguencia Castro
- **Funded by:** Proyecto académico/educativo
- **Shared by:** Daniel Siguencia Castro
- **Model type:** Random Forest Classifier
- **Language(s):** Python
- **License:** MIT
- **Finetuned from model:** Modelo base de scikit-learn RandomForestClassifier

### Model Sources

- **Repository:** [Enlace a tu repositorio de GitHub si tienes]
- **Paper:** Breast Cancer Wisconsin (Diagnostic) Dataset - UCI Machine Learning Repository
- **Demo:** Disponible a través de endpoint en Databricks

## Uses

### Direct Use

Este modelo está diseñado para:
- Clasificación binaria de tumores de mama (benigno vs maligno)
- Herramienta de apoyo para diagnóstico médico
- Investigación y educación en machine learning aplicado a la salud

### Downstream Use

- Integración en sistemas de diagnóstico asistido
- Análisis de características importantes para el cáncer de mama
- Benchmark para comparar otros modelos de clasificación

### Out-of-Scope Use

- ❌ **NO** debe usarse como único método de diagnóstico médico
- ❌ **NO** reemplaza la evaluación de profesionales médicos
- ❌ **NO** apto para diagnóstico en producción sin validación clínica
- ❌ **NO** debe usarse con datos de diferentes fuentes sin reentrenamiento

## Bias, Risks, and Limitations

### Limitaciones Técnicas:
- Entrenado únicamente con el dataset Wisconsin Breast Cancer
- No incluye datos demográficos de pacientes
- Limitado a las 30 características del dataset original
- Precisión del 95.6% - existe margen de error

### Consideraciones Éticas:
- Falsos negativos podrían tener consecuencias graves
- Falsos positivos podrían causar ansiedad innecesaria
- El modelo no considera factores clínicos adicionales

### Recommendations

- **Uso recomendado:** Solo como herramienta de apoyo educativo y de investigación
- **Validación:** Siempre validar predicciones con profesionales médicos
- **Transparencia:** Comunicar claramente las limitaciones del modelo
- **Auditoría:** Realizar pruebas regulares de rendimiento y sesgos

## How to Get Started with the Model

```python
# Cargar el modelo desde MLflow
import mlflow.pyfunc

model = mlflow.pyfunc.load_model("models:/CANCER_DE_MAMA/1")

# Realizar predicción
import pandas as pd
import numpy as np

# Ejemplo de datos de entrada
sample_data = {
    'mean radius': [13.5],
    'mean texture': [21.2],
    'mean perimeter': [88.0],
    'mean area': [559.0],
    'mean smoothness': [0.129]
}

df = pd.DataFrame(sample_data)
prediction = model.predict(df)
print(f"Predicción: {'BENIGNO' if prediction[0] == 1 else 'MALIGNO'}")
