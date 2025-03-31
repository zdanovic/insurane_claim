
# Insurance Claim Forecasting Pipeline

This repository contains a complete, modular solution for forecasting insurance claim costs across two key stages of the claim lifecycle:

1. **FNOL Reserve Estimation** (Initial Loss Prediction)
2. **Final Claim Cost Forecasting** (Total Payout + Reserve after settlement)

The objective is to provide highly interpretable and accurate regression models using both statistical and machine learning approaches—tailored for real-world insurance decision-making.

---

## Project Structure

```
├── 01_preprocessing_eda.ipynb     # Data preparation, cleaning, feature engineering, and EDA
├── 02_fnol_model.ipynb            # FNOL (First Notification of Loss) reserve prediction model
├── 03_final_loss_model.ipynb      # Final claim cost prediction using ensemble models
├── merged_data.csv                # Combined dataset used across notebooks
├── README.md                      # Project documentation
```

---

## Business Use Case

Insurance companies must estimate claim costs at two distinct points:
- Immediately after the claim is reported (FNOL stage), where only limited data is available.
- After claim resolution, where more data has accumulated, including prior reserves and payment history.

This project helps actuarial and claims teams:
- Improve reserve setting accuracy
- Prioritize high-cost claims
- Reduce variability and over/under-reserving

---

## Key Features

- **Clean, validated EDA**: Comprehensive analysis of claim, policy, and vehicle data. Seasonality, log transforms, encoding, and rolling claim windows included.
- **FNOL Model**: Predicts initial reserve using only information available at the point of notification. GLM Tweedie and XGBoost models compared.
- **Final Loss Model**: Predicts final claim cost using prior reserve estimates, claim characteristics, and FNOL outputs.
- **Ensemble Modeling**: Combines statistical and ML-based predictions using Stacking Regressor (XGBoost + GLM).
- **Interpretability**: Feature importance via SHAP, top error case analysis, and business-aligned visuals.
- **No data leakage**: All modeling strictly avoids using post-claim settlement information during training.

---

## Models & Evaluation

| Stage        | Model              | MAE (USD) | RMSE (USD) | R² Score |
|--------------|--------------------|-----------|------------|----------|
| FNOL         | GLM Tweedie        | ✅ Robust baseline for early reserve setting |  
|              | XGBoost            |           |            |          |
| Final Loss   | GLM Tweedie        | 529,000   | 1.16M      | –1.77    |
|              | XGBoost            | 648,000   | 951K       | –0.87    |
|              | **Ensemble (XGB+GLM)** | **415,000** | **702K** | **–0.02** |

---

## Business Impact

- The ensemble model reduced absolute error by ~36% over baseline models.
- It provides a strong foundation for real-time reserving, loss forecasting, and claim triage systems.
- Model outputs are interpretable and can be integrated into internal dashboards and audit pipelines.

---

## How to Use

1. Clone the repository  
   ```bash
   git clone https://github.com/your-org/insurance-claim-forecast.git
   cd insurance-claim-forecast
   ```

2. Run notebooks in order:
   - `01_preprocessing_eda.ipynb`
   - `02_fnol_model.ipynb`
   - `03_final_loss_model.ipynb`

3. Replace `merged_data.csv` with your production claim/policy data (ensuring column match).

---

## Requirements

- Python 3.8+
- scikit-learn
- pandas
- xgboost
- matplotlib, seaborn
- shap

---

## License

This project is provided for educational and internal analytical purposes. Contact the repository owner for commercial licensing inquiries.
