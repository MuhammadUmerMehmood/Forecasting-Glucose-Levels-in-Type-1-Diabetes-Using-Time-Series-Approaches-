# 🩺 Blood Glucose Level Forecasting in Type 1 Diabetes
### MSc Data Science — Final Year Project

![Python](https://img.shields.io/badge/Python-3.10-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![Kaggle](https://img.shields.io/badge/Platform-Kaggle-20BEFF)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)

---

## 📌 Project Overview
The goal of this study is to employ deep learning time series models to predict blood glucose levels in individuals with Type 1 Diabetes (T1D). 
By predicting glucose levels 30 minutes in advance, Continuous Glucose Monitor (CGM) data can assist patients and physicians in taking preventative measures against potentially harmful bouts of hypoglycemia and hyperglycemia.

---

## 🎯 Objectives
Analyse 200 T1D patients' CGM data in an exploratory manner.
Construct and assess three deep learning models: CNN, GRU, and LSTM
MAE, RMSE, and R2 measures are used to compare model performance.
Determine which short-term glucose predicting model is the most accurate.

---

## 📊 Dataset
- **Source:** Clinical CGM dataset — 200 Type 1 Diabetes patients
- **Total Readings:** 647,858 glucose readings
- **Sampling Rate:** Every 5 minutes (continuous)
- **Target Variable:** Blood glucose level (mg/dL)
- **Features:** Demographics, clinical history, medications, comorbidities

### Glucose Zone Distribution:
| Zone | Range | Count | Percentage |
|---|---|---|---|
| 🔴 Hypoglycemia | < 70 mg/dL | 48,839 | 7.5% |
| 🟢 Normal | 70–180 mg/dL | 333,033 | 51.4% |
| 🟠 Hyperglycemia | > 180 mg/dL | 265,986 | 41.1% |

---

## 🏗️ Project Structure
```
📁 t1d-glucose-forecasting
│
├── 📓 notebook.ipynb        # Main Kaggle notebook
├── 📄 README.md             # Project documentation
│
├── 🔷 Section 1: Imports & Configuration
├── 🔷 Section 2: Data Loading
├── 🔷 Section 3: Exploratory Data Analysis (EDA)
├── 🔷 Section 4: Data Preprocessing
├── 🔷 Section 5: Feature Engineering
├── 🔷 Section 6: LSTM Model
├── 🔷 Section 7: GRU Model
├── 🔷 Section 8: CNN Model
└── 🔷 Section 9: Model Comparison & Results
```
## ✅ Current Progress

- [x] Environment Setup & GPU Configuration
- [x] Data Loading & Datetime Parsing
- [x] Exploratory Data Analysis (EDA)
- [x] Outlier Handling
- [x] Normalisation
- [x] Feature Engineering (Lag Features & Rolling Statistics)
- [x] Sequence Creation
- [x] Train / Validation / Test Split
- [x] LSTM Model — Built, Trained & Evaluated
- [x] GRU Model — Built, Trained & Evaluated
- [x] CNN Model — Built, Trained & Evaluated
- [x] Model Comparison & Final Results

---

## 🔬 Models Used
| Model | Type | Why Used |
|---|---|---|
| **LSTM** | Recurrent Neural Network | Captures long-term temporal dependencies in glucose patterns |
| **GRU** | Recurrent Neural Network | Faster, lighter alternative to LSTM with comparable accuracy |
| **CNN** | Convolutional Neural Network | Extracts local temporal patterns from glucose sequences |

---

## 📈 Evaluation Metrics
- **MAE** — Mean Absolute Error (mg/dL)
- **RMSE** — Root Mean Squared Error (mg/dL)
- **R²** — Coefficient of Determination

---

## 🏆 Model Results

| Model | MAE | RMSE | R² |
|---|---|---|---|
| LSTM | 15.4421 | 23.1904 | 0.9263 |
| GRU | 20.3986 | 28.0513 | 0.8922 |
| **CNN** | **14.3097** | **21.6268** | **0.9359** |

🏆 **Best Model: CNN** — Lowest MAE and RMSE, Highest R²

---

## 🛠️ Technologies Used
- **Python 3.10**
- **TensorFlow / Keras** — Deep learning models
- **Pandas & NumPy** — Data manipulation
- **Matplotlib & Seaborn** — Visualizations
- **Scikit-learn** — Preprocessing & metrics
- **Kaggle Notebooks** — GPU-accelerated training

---

## 🔮 Future Plan

- [ ] Hyperparameter Tuning
- [ ] Hybrid Model Exploration
- [ ] Real-time CGM Integration
- [ ] Final Report & Viva

---

## 📚 References
1. Author(s). (2024). Blood glucose level prediction using deep learning models in type 1 diabetes. *PMC National Library of Medicine*. https://pmc.ncbi.nlm.nih.gov/articles/PMC11423977/

2. Jaloli, M., & Cescon, M. (2023). Long-term prediction of blood glucose levels in type 1 diabetes using a CNN-LSTM-based deep neural network. *Journal of Diabetes Science and Technology, 17*(6), 1590–1601. https://doi.org/10.1177/19322968221092785

3. Li, K., Liu, C., Zhu, T., Herrero, P., & Georgiou, P. (2019). GluNet: A deep learning framework for accurate glucose forecasting. *IEEE Journal of Biomedical and Health Informatics, 24*(2), 414–423. https://doi.org/10.1109/JBHI.2019.2931842

4. Anonymous. (2025). Blood glucose level prediction in type 1 diabetes using machine learning. *arXiv*. https://arxiv.org/html/2502.00065v1

---

## 👤 Author
**Muhammad Umer Mehmood**

**23102319**

Final Year Project — 2025/2026
