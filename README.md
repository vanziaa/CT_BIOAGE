# CT-Based Biological Age Model

`final_bioage_model.joblib` is a machine-learning model that estimates **CT-based biological age** from body-composition features extracted from non-contrast thoracoabdominal CT scans.

## Model

The model is an **ElasticNet regression** model selected using mutual-information feature selection. It was developed from CT-derived measurements of organs, vessels, muscle, fat, and bone.

The model stores **43 input feature columns**, of which **37 have non-zero coefficients** and contribute to the predicted age. The remaining six zero-coefficient columns are retained only to preserve the original input schema.

## Input and output

| Item | Description |
|---|---|
| Input | A table of 43 CT-derived features with the names and order stored in `selected_features` |
| Required preprocessing | Apply the same median imputation and z-score normalization used during model training |
| Output | Predicted CT-based biological age in years |

>  Raw CT features must not be passed directly to the model if reproducible predictions are required.

## Minimal usage

```python
import joblib

artifact = joblib.load("final_bioage_model.joblib")
feature_names = artifact["selected_features"]
model = artifact["model"]

# X must be preprocessed and contain the 43 columns in `feature_names` order.
X = X[feature_names]
predicted_biological_age = model.predict(X)
```

The artifact was serialized with **scikit-learn 1.6.1**. A Python 3.10 environment with `joblib`, `numpy`, `pandas`, and `scikit-learn==1.6.1` is recommended.

## Important note

This model is provided for **research use only**. It is not a diagnostic tool and should not be used for clinical decision-making.

## Related manuscript

Yu Q, Hanaoka S, Nomura Y, et al. *CT-based Biological Age as a Biomarker of Aging and Age-related Disease Assessment.* npj Aging.
