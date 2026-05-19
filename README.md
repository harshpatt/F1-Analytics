# F1 Race Performance Analytics

**What:** End-to-end data analytics pipeline on 2024 Formula 1 telemetry — EDA, regression modeling, tire degradation analysis, and driver comparison.

**Personal connection:** Extended my IB Math IA (Piastri vs Verstappen cornering geometry at Suzuka) into a full Python data pipeline using real FastF1 telemetry.

**Stack:** Python · FastF1 · pandas · scikit-learn · matplotlib · seaborn

---

## Questions Answered

- Who was faster — Piastri or Verstappen — and across which sectors at Suzuka?
- How much does tire age affect lap time? (Linear Regression, quantified degradation rate)
- Does the tire compound (Medium vs Hard) create a measurable pace delta?
- Which features best predict a lap time?

---

## Notebooks

| # | Notebook | Concept | Status |
|---|---|---|---|
| 01 | `01_eda_data_loading.ipynb` | EDA, CRISP-DM, Data Quality | ✅ Complete |
| 02 | `02_linear_regression.ipynb` | Linear Regression, MSE, R², Residuals | ✅ Complete |
| 03 | `03_clustering.ipynb` | K-Means, Strategy Groups | 🔄 In progress |
| 04 | `04_classification.ipynb` | Random Forest, Feature Importance | 🔄 In progress |

---

## Key Findings (2024 Japanese GP)

- **VER median lap: 96.393s · PIA median lap: 97.021s** — Verstappen 0.628s faster per lap
- **Tire degradation:** Linear regression quantifies exactly how many seconds each lap on a tire costs (Medium vs Hard compounds separately)
- **Sector 1** (contains the S-curves from the IB IA) shows the largest per-driver delta
- **R² ~0.6–0.8** — 3 features (tire age, compound, lap number) explain majority of lap time variation

---

## Visualizations

### Lap Time Trend — All Race Laps
![Lap Time Trend](outputs/01_lap_time_trend.png)

### Lap Time Distribution
![Distribution](outputs/02_lap_time_distribution.png)

### Sector Time Comparison (Suzuka)
![Sectors](outputs/03_sector_comparison.png)

### Pace by Tire Compound
![Compounds](outputs/04_pace_by_compound.png)

### Regression: Actual vs Predicted
![Regression](outputs/05_actual_vs_predicted.png)

### Tire Degradation Curves
![Degradation](outputs/06_tire_degradation.png)

### Residual Plot
![Residuals](outputs/07_residuals.png)

---

## How to Run

```bash
pip install fastf1 pandas numpy matplotlib seaborn scikit-learn jupyter openpyxl
jupyter notebook 01_eda_data_loading.ipynb
```

Data downloads automatically via FastF1 on first run (~2–5 min). Cached locally after that.

---

## Dataset

Real F1 telemetry via [FastF1](https://docs.fastf1.dev/) — official timing data, lap by lap.  
Race: 2024 Japanese Grand Prix · Suzuka · April 7, 2024.
