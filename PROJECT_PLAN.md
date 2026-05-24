# F1 Analytics Project — Roadmap

**Goal:** Portfolio project for internship applications (Fintech/Data roles).  
**Data:** 2024 Japanese Grand Prix · Suzuka · FastF1 cache already downloaded.  
**Context:** Extends IB Math IA on Piastri vs Verstappen cornering at Turn 1.  
**Deadline:** Apply from Tuesday onwards (week of 2026-05-19).

---

## 4 Notebooks — One Course Concept Each

| # | File | Course Concept | F1 Angle | Status |
|---|------|---------------|----------|--------|
| 01 | `01_eda_data_loading.ipynb` | EDA, Data Quality, CRISP-DM | Lap time distributions, sector splits, Piastri vs Verstappen | ✅ Written |
| 02 | `02_linear_regression.ipynb` | Linear Regression (Modeling II) | Predict lap time from tire age + lap number + weather | ✅ Written |
| 03 | `03_clustering.ipynb` | K-Means Clustering (Modeling III) | Group drivers by driving style (tire deg rate, sector performance) | ⬜ Pending |
| 04 | `04_classification.ipynb` | Decision Tree / Random Forest (Modeling I/II) | Classify lap type: push lap / in-lap / out-lap from telemetry features | ⬜ Pending |

---

## CRISP-DM Mapping

```
Business Understanding  → "How did Piastri vs Verstappen compare? Can we predict/classify F1 laps?"
Data Understanding      → Notebook 01 (EDA)
Data Preparation        → Done inside each notebook (cleaning, feature engineering)
Modeling                → Notebooks 02, 03, 04
Evaluation              → End of each notebook (metrics: MSE, R², silhouette, accuracy)
Deployment              → Not needed for portfolio — charts + summary are the output
```

---

## Folder Structure

```
f1-analytics/
├── PROJECT_PLAN.md          ← this file
├── 01_eda_data_loading.ipynb
├── 02_linear_regression.ipynb
├── 03_clustering.ipynb           (not yet created)
├── 04_classification.ipynb       (not yet created)
├── outputs/                      ← all saved charts go here
│   ├── 01_lap_time_trend.png
│   ├── 02_lap_time_distribution.png
│   ├── 03_sector_comparison.png
│   └── 04_pace_by_compound.png
└── cache/                        ← FastF1 cache (2024 Japanese GP already downloaded)
    └── 2024/2024-04-07_Japanese_Grand_Prix/
```

---

## Notebook 01 — What Was Built

**Steps written:**
1. Import libraries
2. Enable FastF1 cache
3. Load 2024 Japanese GP Race session
4. Data Understanding — `.shape`, `.columns`, `.head()`
5. Data Quality — missing value check, `pick_accurate()` to remove pit/SC laps
6. Filter to Verstappen (`VER`) and Piastri (`PIA`), convert LapTime to seconds
7. Descriptive stats — `.describe()` on both drivers
8. Chart 1 — Lap time trend (line chart, all laps)
9. Chart 2 — Lap time distribution (box plot)
10. Chart 3 — Sector time comparison (bar chart, median per sector)
11. Chart 4 — Pace by tire compound (grouped box plot)
12. EDA summary printout

**Course concepts demonstrated:** CRISP-DM, EDA, Data Quality (completeness, accuracy), Data Transformation (timedelta → float), Anscombe lesson (visualize before stats).

---

## Notebook 02 — Plan (Linear Regression)

**Question:** Can we predict a driver's lap time given tire age, lap number, and compound?

**Features (X):**
- `TyreLife` — how many laps the tire has done (proxy for degradation)
- `LapNumber` — proxy for fuel load (lighter car = faster as race progresses)
- `Compound_encoded` — tire type as a number (Soft=0, Medium=1, Hard=2)

**Target (y):** `LapTimeSec`

**Steps to build:**
1. Feature engineering — encode compound, drop nulls
2. Train/test split (80/20)
3. Normalization/standardization (from course Session 2)
4. Fit `LinearRegression` from sklearn
5. Plot: actual vs predicted lap times
6. Metrics: MSE, R² — explain what they mean
7. Plot: residuals (errors) — check for patterns
8. Interpret coefficients — "each extra lap on tire adds X seconds"

---

## Notebook 03 — Plan (K-Means Clustering)

**Question:** Can we cluster all drivers into groups by their driving style — who pushes hard early, who manages tires?

**Features:**
- Sector 1 median time (high-speed aero performance)
- Sector 2 median time (braking + slow corners)
- Tire degradation rate (slope of lap time vs TyreLife)
- Avg pace relative to their own best lap

**Steps:**
1. Build feature matrix — one row per driver
2. Standardize (K-Means is distance-based — scaling is critical, from course)
3. Elbow method to find optimal k
4. Fit KMeans, assign cluster labels
5. Visualize clusters (scatter plot, PCA if needed)
6. Interpret: what does each cluster represent?

---

## Notebook 04 — Plan (Decision Tree / Random Forest)

**Question:** Can we classify each lap as a push lap, in-lap, or out-lap using telemetry features?

**Features:**
- `LapTimeSec` relative to driver median
- `TyreLife`
- `Sector1Sec`, `Sector2Sec`, `Sector3Sec`
- `SpeedST` (speed trap)

**Target:** Lap type label (engineered from the data)

**Steps:**
1. Engineer labels — define what counts as in-lap/out-lap/push lap
2. Train/test split
3. Fit DecisionTreeClassifier, then RandomForestClassifier
4. Compare accuracy
5. Plot decision tree (interpretable — good for portfolio)
6. Feature importance chart — which feature matters most?

---

## Teaching Approach

Every notebook: **explain before code, explain after output.**
- Why we write each line
- What the output tells us
- How it connects to the course concept
- One chart saved to `outputs/` per visualization
