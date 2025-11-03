# For reference on model card metadata, see the spec: https://github.com/huggingface/hub-docs/blob/main/modelcard.md?plain=1
# Doc / guide: https://huggingface.co/docs/hub/model-cards
---
tags:
- classification
- breast-cancer
- medical
- tabular-data
- mlflow
datasets:
- breast-cancer-wisconsin # Asunción basada en el contexto médico
library_name: scikit-learn # Asunción, común para clasificación inicial. Si es otro, debe ser actualizado.
license: mit
---

# Model Card for Modelo_Clasificacion_Cancer_Mama

Modelo de Machine Learning entrenado para la **clasificación binaria** de tumores de cáncer de mama. Su propósito es clasificar una muestra de tejido como **Benigno** o **Maligno** basado en las características celulares.

## Model Details

### Model Description

Este modelo es un prototipo inicial desarrollado para la tarea de clasificación diagnóstica de cáncer de mama. Fue entrenado para predecir si un tumor es maligno o benigno a partir de características tabulares extraídas del análisis celular. El entrenamiento fue rastreado usando **MLflow**.

- **Developed by:** [More Information Needed]
- **Funded by [optional]:** [More Information Needed]
- **Shared by [optional]:** [More Information Needed]
- **Model type:** Classification Model (Tipo específico: [Ej. Logistic Regression / Random Forest / SVM])
- **Language(s) (NLP):** [N/A - Datos Numéricos/Tabulares]
- **License:** MIT
- **Finetuned from model [optional]:** [N/A]

### Model Sources [optional]

- **Repository:** [More Information Needed]
- **Paper [optional]:** [More Information Needed]
- **Demo [optional]:** El modelo está publicado en un *Serving Endpoint* de Databricks para inferencia.

## Uses

### Direct Use

El uso principal es la **investigación** y **prueba de concepto (Proof of Concept)** en el área de la oncología o el *Machine Learning* aplicado a la salud, para evaluar la viabilidad de la clasificación de cáncer de mama con modelos ML.

### Downstream Use [optional]

Podría integrarse en una herramienta más grande de apoyo a la decisión clínica, pero solo después de una validación exhaustiva y bajo estricta supervisión regulatoria.

### Out-of-Scope Use

**USO CRÍTICO FUERA DE ALCANCE:** **NO DEBE UTILIZARSE BAJO NINGUNA CIRCUNSTANCIA PARA DIAGNÓSTICO MÉDICO O TRATAMIENTO DIRECTO EN HUMANOS.** El modelo es un prototipo con un dataset limitado y no sustituye el juicio de un profesional médico calificado. Su uso irresponsable puede llevar a un diagnóstico erróneo con graves consecuencias.

## Bias, Risks, and Limitations

El riesgo y la limitación más significativos es el **tamaño limitado del dataset de entrenamiento (455 muestras)**. Esto puede resultar en:
1.  **Baja Capacidad de Generalización:** El modelo podría estar sobreajustado y fallar al aplicarse a poblaciones o datos con distribuciones diferentes.
2.  **Sesgo de Muestreo:** Si el dataset original proviene de una región o un subgrupo demográfico específico, el modelo puede exhibir un rendimiento sesgado en otros grupos.
3.  **Dependencia del Endpoint:** El código de inferencia depende de un *Serving Endpoint* específico de Databricks, incluyendo una URL y un token de acceso, lo que añade complejidad operacional y de seguridad.

### Recommendations

Users (both direct and downstream) should be made aware of the risks, biases and limitations of the model. **Se recomienda encarecidamente aumentar el tamaño del conjunto de datos de entrenamiento** a miles de muestras para mejorar la solidez y la capacidad de generalización del modelo.

## How to Get Started with the Model

Utilice la siguiente estructura de código para realizar la inferencia. **Recuerde no exponer la URL y el token en código plano.**

```python
import pandas as pd
import requests
import json
# ... (función create_tf_serving_json si el formato de entrada no es pandas)

def score_model(dataset):
    # La URL y el token deben ser obtenidos de variables de entorno (secrets)
    url = '[https://dbc-c588324d-9eb4.cloud.databricks.com/serving-endpoints/CANCER_DE_MAMA/invocations](https://dbc-c588324d-9eb4.cloud.databricks.com/serving-endpoints/CANCER_DE_MAMA/invocations)' 
    headers = {'Authorization': f'Bearer {YOUR_SECRET_TOKEN}', 'Content-Type': 'application/json'}
    
    # Prepara el dataset de entrada
    ds_dict = {'dataframe_split': dataset.to_dict(orient='split')} 
    data_json = json.dumps(ds_dict, allow_nan=True)
    
    # Envía la solicitud al endpoint
    response = requests.request(method='POST', headers=headers, url=url, data=data_json)
    
    if response.status_code != 200:
        raise Exception(f'Request failed with status {response.status_code}, {response.text}')
    
    return response.json()
