# EV Charging Energy Consumption Prediction — Phase 2

This repository contains a reproducible baseline implementation for the Machine Learning coursework (Phase 2, Option A) based on Hussain et al. (2025).

## Research reference
Hussain, I., Ching, K. B., Uttraphan, C., Tay, K. G., & Noor, A. (2025). *Evaluating machine learning algorithms for energy consumption prediction in electric vehicles: A comparative study*. Scientific Reports, 15, Article 16124. https://doi.org/10.1038/s41598-025-94946-7

## Repository structure

```text
ev-energy-ml-phase2/
├── data/
│   ├── raw/
│   └── processed/           
├── notebooks/
│   └── ML_CW_Phase_2_EV_Energy_Prediction_Revised.ipynb
├── outputs/
├── reports/
│   └── Phase_2_Technical_Application_Report.pdf
├── figures/
├── requirements.txt
├── .gitignore
└── README.md
```

## Environment

Python 3.10+ is recommended. Install dependencies:

```bash
python -m venv .venv
# Windows PowerShell:
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## Run in Google Colab

1. Upload `notebooks/ML_CW_Phase_2_EV_Energy_Prediction_Revised.ipynb` to Colab.
2. Upload the dataset privately to the Colab session, or mount Drive if appropriate.
3. Update `DATA_PATH` in the configuration cell to the actual dataset path.
4. Run all cells from top to bottom.
5. Inspect the detected column mapping, duplicate-row audit, train/test periods and warnings.
6. Download the newly generated `phase2_model_comparison_results.csv` and `phase2_chronological_test_predictions.csv` and replace the previous-run exports only after checking them.

## Models and evaluation

- Dummy median regression baseline
- Random Forest regression
- Extra Trees regression
- Random 80/20 split for a paper-style comparison
- Chronological hold-out that keeps identical start timestamps in one partition
- Optional expanding-window temporal cross-validation on the training period
- MAE, MSE, RMSE, R² and test-range-normalised RMSE

## Important limitations

- The published paper's metrics are references, not this repository's measured results.
- The `outputs/previous_run/` files came from the earlier notebook version. They must not be described as outputs of the revised notebook.
- The revised notebook changes the chronological split boundary and temporal cross-validation folds to keep identical timestamps together. Rerun it before final submission; results may change.
- Duration features may not be available before a charging session begins. Define the prediction time and feature availability before claiming real-time or pre-session forecasting.
- Exact duplicate source rows are audited but not automatically removed. Confirm whether they represent true duplicate sessions before deciding how to handle them.
- Do not upload the raw dataset if its licence, terms, or size make redistribution inappropriate.

## Published reference values

The paper abstract reports Extra Trees MAE = 0.5888 kWh, MSE = 3.2683 kWh², R² = 0.9592, RMSE = 1.8078 kWh, and NRMSE = 0.0200. Verify the original paper when citing these values.

