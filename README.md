#  Forecasting Glucose Levels in Type 1 Diabetes Using Machine Learning

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?logo=tensorflow)](https://www.tensorflow.org/)
[![Keras](https://img.shields.io/badge/Keras-3.x-red?logo=keras)](https://keras.io/)
[![Kaggle](https://img.shields.io/badge/Kaggle-Notebook-20BEFF?logo=kaggle)](https://www.kaggle.com/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

> **Student:** Muhammad Umer Mehmood · **ID:** 23102319 · **Supervisor:** Ralf Napiwotzki

A deep learning project that forecasts blood glucose levels **30 minutes ahead** using Continuous Glucose Monitoring (CGM) data from 200 Type 1 Diabetes patients. Three architectures — **LSTM, GRU, and CNN** — are trained and compared on 647,858 real-world glucose readings.

---

## Results at a Glance

| Model | MAE (mg/dL) ↓ | RMSE (mg/dL) ↓ | R² ↑ |
|-------|:---:|:---:|:---:|
| 🥇 **GRU** | **13.80** | **19.90** | **0.9450** |
| 🥈 LSTM | 13.96 | 19.96 | 0.9447 |
| 🥉 CNN | 14.63 | 20.33 | 0.9426 |

All three models achieve **R² > 0.94**, demonstrating that deep learning effectively captures the complex, non-linear temporal dynamics of CGM glucose data.

---

##  Repository Structure

```
├── gcm-using-machine-learning-models.ipynb   # Main Kaggle notebook
├── best_lstm.keras                            # Saved best LSTM model weights
├── README.md
└── weinstock.csv                              # Dataset (GlucoBench — add to Kaggle input)
```

---

##  Dataset

**Source:** [GlucoBench](https://github.com/IrinaStatsLab/GlucoBench) — longitudinal CGM records

| Property | Value |
|---|---|
| Patients | 200 |
| Total Readings | 647,858 |
| Sampling Interval | Every 5 minutes |
| Glucose Range | 40 – 400 mg/dL (clipped) |
| Key Column | `gl` (glucose in mg/dL) |

---

##  Project Pipeline

```
Raw CGM Data
    │
    ▼
1. Exploratory Data Analysis
   ├── Glucose distribution & zone analysis (hypo / normal / hyper)
   ├── Per-patient statistics & variability
   ├── Diurnal (hour-of-day) patterns
   ├── Autocorrelation & stationarity (ADF test)
   └── Time gap analysis
    │
    ▼
2. Data Preprocessing
   ├── Glucose clipping (40–400 mg/dL)
   ├── Feature engineering (lags, diffs, rolling stats, hour)
   ├── MinMax normalisation (separate scaler for glucose)
   ├── Sliding-window sequence creation (with gap handling)
   └── Time-based 70 / 15 / 15 train-val-test split
    │
    ▼
3. Model Training
   ├── LSTM  →  LSTM(64) → Dropout → LSTM(32) → Dropout → Dense(32) → Dense(6)
   ├── GRU   →  GRU(64)  → Dropout → GRU(32)  → Dropout → Dense(32) → Dense(6)
   └── CNN   →  Conv1D(64) → MaxPool → Conv1D(32) → Flatten → Dense(32) → Dense(6)
    │
    ▼
4. Evaluation & Comparison
   ├── MAE, RMSE, R² on test set
   └── Per-horizon error analysis (5 → 30 min)
```

---

##  Model Architecture (LSTM — Best Saved Model)

```
Input: (None, 12, 12)   →   12 timesteps × 12 features (1 hour of history)

┌─────────────────────────────────────┐
│  LSTM  (64 units, return_seq=True)  │
│  Dropout (0.2)                      │
│  LSTM  (32 units)                   │
│  Dropout (0.2)                      │
│  Dense (32, ReLU)                   │
│  Dense (6, Linear)                  │
└─────────────────────────────────────┘

Output: (None, 6)   →   6 glucose values = next 30 minutes
```

**Training Config:** Adam (lr=0.001) · Loss: MSE · Metric: MAE · Epochs: 100 · EarlyStopping (patience=10)

---

## ⚙️ Features Used

| Feature | Description |
|---|---|
| `gl` | Raw glucose (mg/dL) |
| `gl_lag1/2/3` | Glucose 5, 10, 15 minutes ago |
| `gl_diff1/2` | Rate of change over 1–2 steps |
| `rolling_mean_6/12/36` | Rolling mean over 30, 60, 180 min |
| `rolling_std_6/12` | Rolling std (variability) |
| `hour` | Hour of day (diurnal pattern) |

---

##  Quick Start on Kaggle

### 1. Upload the dataset
Add `weinstock.csv` as a Kaggle dataset and note the dataset slug.

### 2. Load the saved LSTM model
```python
import tensorflow as tf

model = tf.keras.models.load_model("/kaggle/input/your-dataset-name/best_lstm.keras")
model.summary()
```

### 3. Run inference
```python
import numpy as np

# Input: 1 sample, 12 timesteps, 12 features
X_sample = np.random.rand(1, 12, 12)
predictions = model.predict(X_sample)

print("Predicted glucose (next 30 min, scaled):", predictions)
# Remember to inverse-transform using your gl_scaler to get mg/dL values
```

### 4. Install dependencies (if running locally)
```bash
pip install tensorflow numpy pandas matplotlib seaborn scikit-learn statsmodels
```

---

##  Key Findings

- **GRU is the best model** — its simpler gating mechanism proves sufficient for this task while being faster to train than LSTM.
- **All models achieve R² > 0.94** — deep learning reliably captures the non-linear temporal dynamics of CGM data.
- **Prediction accuracy degrades with horizon** — the first 10–15 minutes are the most accurate; error rises toward the 30-minute mark.
- **CNN ranks third** — parallel convolution is fast but lacks the sequential memory advantage of recurrent architectures for this task.

---

##  Limitations

- Placeholder dates (year 1900) in the dataset limit reliability of date-based features.
- A global model may not optimally serve all patients — personalised fine-tuning could improve results.
- No insulin dosing or meal data included, both of which heavily influence glucose dynamics.

---

##  Future Work

- Explore hybrid architectures (CNN-GRU) and Transformer-based models with attention.
- Develop patient-specific models using transfer learning.
- Integrate insulin dosing and carbohydrate intake data.
- Deploy predictions into a real-time CGM application for clinical use.

---

##  Tech Stack

`Python` · `TensorFlow / Keras` · `NumPy` · `Pandas` · `Scikit-learn` · `Matplotlib` · `Seaborn` · `Statsmodels`

---

##  License

This project is for academic purposes. Dataset credit: [GlucoBench](https://github.com/IrinaStatsLab/GlucoBench).
