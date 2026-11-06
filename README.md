# qml-heart

Reproduction code for:

**Benchmarking quantum machine learning against classical models for the diagnostic classification of obstructive
coronary artery disease in the UCI Heart Disease cohorts: an internal–external validation study with ablation,
conformal prediction and simulated noise sensitivity analysis.**

## Contents

| File | Purpose |
|---|---|
| `QML_Heart_Reproduction_Pipeline.ipynb` | Self-contained notebook holding all analysis and audit code |
| `requirements.txt` | Pinned software versions used for the reported results |

## How to reproduce

**Google Colab:** open the notebook in Colab and choose *Runtime → Run all*. If the first cell reports that
NumPy/pandas were changed, choose *Runtime → Restart session* once and run all cells again.

**Locally (Python 3.12 or 3.13):**

```bash
pip install -r requirements.txt jupyter
jupyter nbconvert --to notebook --execute --ExecutePreprocessor.timeout=-1 QML_Heart_Reproduction_Pipeline.ipynb
```

The notebook

1. downloads the original UCI Heart Disease files (dataset 45; Cleveland, Hungarian, VA Long Beach, Zurich) and
   checks their SHA-256 hashes;
2. runs every analysis of the article with fixed random seeds: six classical models, four quantum models and two
   matched-input comparators, internal and external validation, conformal prediction, gradient variance,
   gate-level noise simulation, ablation, paired bootstrap comparisons and learning curves;
3. regenerates figures 1–8 and S1–S3 and tables 1, 2 and S1–S7 (CSV and Excel);
4. checks 229 key values and every table cell against the article and runs an independent audit;
5. packages all outputs in `qml_heart_reproduction_outputs.zip`.

A full run takes about 30–45 minutes on one CPU core. Set `RUN_LEARNING_CURVES = False` in the first code cell for a
shorter run. Computing times reported in the article depend on the hardware; all other values are reproduced exactly.

## Data

UCI Machine Learning Repository, Heart Disease (dataset 45), CC BY 4.0. A widely circulated third-party re-upload of
the Cleveland records is downloaded only for the data-provenance check; its outcome label is inverted relative to the
original file and it is not used for modelling.
