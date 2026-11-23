# Course Cancellation Prediction | Nova Academy

**End-to-End Machine Learning Project | Tel Aviv University | 2025**

## Business Problem
Nova Academy is a professional training company that commits resources (such as cloud environments, catering, and training kits) before courses begin. Cancellations can waste these resources. The project predicts the risk that a confirmed registration will be cancelled, supporting earlier outreach and more selective resource planning.

**Target:** `Dropped_Course` (1 = cancelled, 0 = attended). The output is a predicted cancellation probability.

## Dataset
The training data contains **63,464 registrations** with 29 raw fields, including booking lead time, course logistics, client history, and payment terms. Approximately **41.4%** of training registrations were cancelled.

The course-provided datasets are **not redistributed** in this repository. To run the notebook, place authorized copies of `Train_Data.csv` and `Test_Data_No_Target.csv` in a local `data/` directory.

## Workflow
1. Business understanding and exploratory data analysis.
2. Data quality checks, including anomalous numeric values and inconsistent categorical labels.
3. Stratified training/validation split (80/20), with preprocessing parameters learned on the training portion.
4. Missing-value imputation, IQR-based clipping, text normalization, categorical encoding and numeric scaling.
5. Investigation of possible target leakage; `Assigned_Lab_Config` was excluded.
6. Training, cross-validation and hyperparameter tuning of Logistic Regression, Random Forest and XGBoost.
7. Model comparison, SHAP interpretation and prediction generation.

## Models and Results
The **notebook's final comparison** reports the following validation ROC-AUC values:

| Model | Validation ROC-AUC |
|---|---:|
| Logistic Regression | 0.8943 |
| Random Forest | 0.9425 |
| **XGBoost** | **0.9445** |

XGBoost was selected as the final model. These values are taken from the notebook's saved analysis and have **not been independently reproduced** in a clean environment.

**Reporting note:** The separately submitted summary report lists a different set of tuned validation AUC scores (0.8917, 0.9314 and 0.9364). The README uses the notebook's final comparison; the difference should be reconciled before claiming a single independently verified result.

## Key Findings
- `Payment_Terms`, particularly prepaid non-refundable registrations, was the strongest reported predictor of cancellations.
- Booking lead time and tuition cost were also informative.
- Strong dependence on payment terms merits monitoring if business policies or data capture practices change.
- The model is intended to support operational prioritization, not automatic cancellation decisions.

## Limitations and Future Work
- Validate with a **time-based** split to better simulate future bookings.
- Calibrate predicted probabilities before treating scores as absolute cancellation risks.
- Test whether interventions on high-risk bookings actually reduce cancellations.
- Monitor feature stability and potential leakage when moving toward production.

## Repository Contents
- `course_cancellation_analysis.ipynb` — analysis, modeling and interpretation (outputs cleared for public sharing)
- `requirements.txt` — main dependencies
- `.gitignore` — excludes data, local outputs and temporary files

## How to Run
1. Install Python and JupyterLab or Jupyter Notebook.
2. Run `pip install -r requirements.txt`.
3. Create a folder named `data` in the repository directory.
4. Put authorized `Train_Data.csv` and `Test_Data_No_Target.csv` files inside `data/`.
5. Open `course_cancellation_analysis.ipynb` and run cells in order.

The notebook was adapted from a Google Colab submission to use relative file paths. A complete end-to-end rerun has **not** been verified.

## Academic Context
Introduction to Machine Learning — Tel Aviv University. Independently completed academic project.
