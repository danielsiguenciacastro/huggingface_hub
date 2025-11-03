language: 
  - es
  - en
tags:
  - medical
  - breast-cancer
  - classification
  - random-forest
  - healthcare
widget:
  - text: "mean_radius: 13.5, mean_texture: 21.2, mean_perimeter: 88.0, mean_area: 559.0, mean_smoothness: 0.129"
license: mit
datasets:
  - breast-cancer-wisconsin
metrics:
  - accuracy
  - f1
---

# CANCER_DE_MAMA - Breast Cancer Classification Model

## Model Description

CANCER_DE_MAMA is a machine learning model based on Random Forest designed to classify breast tumors as benign or malignant using medical features extracted from biopsy images.

- **Developed by:** Daniel Siguencia Castro
- **Funded by:** Proyecto académico/educativo
- **Shared by:** Daniel Siguencia Castro
- **Model type:** Random Forest Classifier
- **Language(s):** Python
- **License:** MIT
- **Finetuned from:** scikit-learn RandomForestClassifier base model

## Model Sources

- **Repository Databricks:** [https://dbc-c588324d-9eb4.cloud.databricks.com/editor/notebooks/3860614997942453](https://dbc-c588324d-9eb4.cloud.databricks.com/editor/notebooks/3860614997942453)
- **Serving Endpoint:** [https://dbc-c588324d-9eb4.cloud.databricks.com/serving-endpoints/CANCER_DE_MAMA/invocations](https://dbc-c588324d-9eb4.cloud.databricks.com/serving-endpoints/CANCER_DE_MAMA/invocations)
- **Paper:** Breast Cancer Wisconsin (Diagnostic) Dataset - UCI Machine Learning Repository

## Intended Uses & Limitations

### Direct Use

This model is designed for:
- Binary classification of breast tumors (benign vs malignant)
- Medical diagnosis support tool
- Research and education in machine learning applied to healthcare

### Downstream Use
- Integration in computer-aided diagnosis systems
- Analysis of important features for breast cancer
- Benchmark for comparing other classification models

### Out-of-Scope Use
- ❌ Should NOT be used as the sole medical diagnostic method
- ❌ Does NOT replace evaluation by medical professionals
- ❌ NOT suitable for production diagnosis without clinical validation
- ❌ Should NOT be used with data from different sources without retraining

## Bias, Risks, and Limitations

### Technical Limitations:
- Trained only with the Wisconsin Breast Cancer dataset
- Does not include patient demographic data
- Limited to the 30 features of the original dataset
- Accuracy of 95.6% - there is margin for error

### Ethical Considerations:
- False negatives could have serious consequences
- False positives could cause unnecessary anxiety
- The model does not consider additional clinical factors

### Recommendations
- **Recommended use:** Only as an educational and research support tool
- **Validation:** Always validate predictions with medical professionals
- **Transparency:** Clearly communicate model limitations
- **Audit:** Conduct regular performance and bias testing
