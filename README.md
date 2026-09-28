# E-Commerce Customer Intelligence and Sales Forecasting

Personal project: can customer-behaviour data explain and forecast e-commerce sales, and do customers fall into meaningful segments?

## Data

Three public datasets: customer behaviour, customer segmentation (1,000 customers) and daily sales transactions, cleaned and integrated in `notebooks/01–04`.

## Method

1. **Segmentation:** K-Means, hierarchical clustering and DBSCAN on standardised customer features; compared with silhouette and Davies–Bouldin scores.
2. **Sales forecasting:** lag features, rolling statistics and seasonality encodings; linear regression, random forest and XGBoost evaluated on a held-out test set.

## Results

**Segmentation**

| Method | Clusters | Silhouette | Davies–Bouldin |
|---|---|---|---|
| K-Means (selected) | 4 | 0.154 | 1.75 |
| Hierarchical | 4 | 0.134 | 1.79 |
| DBSCAN | 15 (898 noise points) | 0.369 | — |

K-Means produced interpretable profiles (e.g. a small premium segment, frequent value seekers, mid-tier moderate spenders), but low silhouette scores mean the segments overlap heavily. DBSCAN's higher score comes from labelling most customers as noise, so it was not used.

**Sales forecasting (test set)**

| Model | MAE | RMSE | R² | MAPE |
|---|---|---|---|---|
| Random forest | 10,311 | 12,209 | 0.03 | 4.8% |
| XGBoost | 10,467 | 12,554 | −0.03 | 4.9% |
| Linear regression | 12,358 | 15,648 | −0.60 | 5.9% |

## Takeaway

This is largely a **negative result**: engineered lag and seasonality features explained almost none of the day-to-day variation in sales (R² ≈ 0), and the customer segments are weakly separated. A low MAPE here reflects a stable sales level, not predictive skill. Useful next steps would be exogenous drivers (promotions, pricing, traffic) and a naive seasonal baseline to benchmark against.

## Repository

```
data/        raw and cleaned datasets
notebooks/   01–03 EDA, 04 integration, 05 sales prediction model
models/      best_sales_model.pkl
results/     notes on outputs (tables above)
```

Tools: Python, pandas, scikit-learn, XGBoost, Matplotlib, Seaborn.
