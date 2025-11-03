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

# Ejemplo de datos de entrada (primeras 5 características mostradas)
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
```

## Training Details

### Training Data

**Dataset:** Breast Cancer Wisconsin (Diagnostic) Dataset
- **Muestras totales:** 569
- **Características:** 30
- **Clases:** 2 (Benigno: 357, Maligno: 212)
- **División:** 80% entrenamiento (455), 20% prueba (114)

### Training Procedure

#### Preprocessing
- Datos ya normalizados en el dataset original
- Split estratificado para mantener proporción de clases
- No se requirió imputación de valores faltantes

#### Training Hyperparameters
```python
{
    "n_estimators": 100,
    "max_depth": None,
    "min_samples_split": 2,
    "random_state": 42
}
```

## Evaluation

### Testing Data, Factors & Metrics

#### Testing Data
- 114 muestras de prueba (20% del dataset original)
- Distribución balanceada manteniendo proporción de clases

#### Metrics
- **Accuracy:** Precisión general del modelo
- **F1-Macro:** Media armónica de precisión y recall (balanceada)

### Results

**Métricas de rendimiento:**
- **Accuracy:** 95.6%
- **F1-Macro:** 95.3%

#### Matriz de Confusión:
```
            Predicción
            Benigno  Maligno
Real Benigno   70       2
Real Maligno    3      39
```

#### Summary
El modelo muestra excelente rendimiento con alta precisión y buen balance entre las dos clases. Los falsos negativos (3) son mínimos pero críticos en el contexto médico.

## Model Examination

### Feature Importance
Las características más importantes para la clasificación incluyen:
- `worst area`
- `worst perimeter` 
- `mean concave points`
- `worst radius`
- `mean area`

### Interpretabilidad
- Random Forest proporciona importancia de características
- Posibilidad de analizar árboles individuales para explicaciones

## Environmental Impact

- **Hardware Type:** CPU estándar
- **Hours used:** < 1 hora de entrenamiento
- **Cloud Provider:** Databricks
- **Compute Region:** [Especificar región si se conoce]
- **Carbon Emitted:** Estimado < 0.1 kg CO₂eq

## Technical Specifications

### Model Architecture and Objective
- **Algoritmo:** Random Forest Classifier
- **Número de árboles:** 100
- **Profundidad máxima:** Sin límite
- **Objetivo:** Minimizar error de clasificación binaria

### Compute Infrastructure

#### Hardware
- Requisitos mínimos: 2GB RAM, 2 cores CPU
- Entrenamiento en cloud computing

#### Software
- Python 3.12
- scikit-learn 1.3+
- MLflow 2.0+
- pandas, numpy

## Citation

**BibTeX:**
```bibtex
@misc{breastcancerwisconsin,
  title={Breast Cancer Wisconsin (Diagnostic) Data Set},
  author={Wolberg, W. and Street, N. and Mangasarian, O.L.},
  year={1995},
  publisher={UCI Machine Learning Repository}
}
```

**APA:**
Wolberg, W., Street, N., & Mangasarian, O.L. (1995). Breast Cancer Wisconsin (Diagnostic) Data Set. UCI Machine Learning Repository.

## Glossary

- **Benigno:** Tumor no canceroso
- **Maligno:** Tumor canceroso
- **Accuracy:** Porcentaje de predicciones correctas
- **F1-Score:** Media armónica entre precisión y recall
- **Feature Importance:** Medida de qué características son más relevantes para las predicciones

## More Information

- **Dataset Source:** https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic)
- **MLflow Tracking:** Experimentos registrados en plataforma Databricks
- **Versión del modelo:** 3 (actual)

## Model Card Authors

Daniel Siguencia Castro - Desarrollador del modelo

## Model Card Contact

Para preguntas técnicas: [tu email]
Para consideraciones éticas: [contacto apropiado]

---

**Nota importante:** Esta Model Card debe actualizarse si el modelo se reentrena con nuevos datos o si se descubren limitaciones adicionales.
