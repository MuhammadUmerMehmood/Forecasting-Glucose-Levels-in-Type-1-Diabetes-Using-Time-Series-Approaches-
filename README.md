---

# Forecasting Glucose Levels in Type 1 Diabetes Using Machine Learning

**Student:** Muhammad Umer Mehmood | **Student ID:** 23102319 | **Supervisor:** Ralf Napiwotzki
**Institution:** University of Hertfordshire | **Programme:** MSc Data Science

---

## Project Overview

This project investigates the application of deep learning to forecast blood glucose levels 30 minutes ahead for patients with Type 1 Diabetes. The dataset originates from Continuous Glucose Monitoring (CGM) devices worn by 200 patients, comprising 647,858 real-world glucose readings.

Three model architectures, LSTM, GRU, and CNN, were developed and benchmarked to determine which best captures the temporal dynamics inherent in glucose time series data.

---

## Results Summary

All three models achieved an R² above 0.94, demonstrating strong predictive performance. The GRU outperformed the other architectures with the lowest error metrics, followed closely by the LSTM and then the CNN.

| Model | MAE (mg/dL) | RMSE | R² |
|-------|-------------|------|----|
| GRU   | 13.80       | 19.90 | 0.9450 |
| LSTM  | 13.96       | 19.96 | 0.9447 |
| CNN   | 14.63       | 20.33 | 0.9426 |

---

## Dataset

The dataset is sourced from **GlucoBench**, a longitudinal CGM benchmark collection curated by IrinaStatsLab. It covers 200 patients with glucose readings recorded every 5 minutes. All values are clipped to a clinically valid range of 40 to 400 mg/dL.

---

## Project Pipeline

The project follows a structured machine learning workflow across four stages.

**1. Exploratory Data Analysis** Examination of glucose distributions, identification of hypoglycaemic and hyperglycaemic zones, analysis of per-patient variability, and detection of temporal gaps in the data.

**2. Data Preprocessing** Glucose value clipping, feature engineering (lag features, rolling statistics, rate-of-change), normalisation, and time-based train/validation/test splitting using a 70/15/15 ratio.

**3. Model Training** Three architectures (LSTM, GRU, CNN) were trained with dropout regularisation, the Adam optimiser, and early stopping to prevent overfitting.

**4. Evaluation** All models were assessed on the held-out test set using MAE, RMSE, and R², with a per-horizon breakdown covering predictions from 5 to 30 minutes ahead.

---

## Model Architecture

Each model accepts 12 timesteps (one hour of historical data) and 12 input features, producing 6 output values representing glucose levels over the next 30 minutes.

**LSTM and GRU:** Two stacked recurrent layers with dropout, followed by two fully connected dense layers.

**CNN:** Two convolutional layers with max pooling, followed by two dense layers.

All models were trained using the Adam optimiser (learning rate: 0.001), MSE loss function, and early stopping with a patience of 10 epochs over a maximum of 100 epochs.

---

## Feature Engineering

The following features were used as model inputs:

- Raw CGM glucose readings
- Lagged glucose values at 5, 10, and 15-minute intervals
- Rate of change over one and two timesteps
- Rolling mean and standard deviation over 30, 60, and 180-minute windows
- Hour of day to capture circadian glucose patterns

---

## Key Findings

The GRU model demonstrated the best overall performance. Its comparatively simpler gating mechanism proved sufficient to capture the temporal dynamics of glucose data while training faster than the LSTM.

Prediction accuracy was highest in the 0 to 15 minute forecast window and degraded progressively toward the 30-minute horizon, consistent with expected behaviour in multi-step time series forecasting.

The CNN, while computationally efficient, ranked third due to its lack of sequential memory, a notable limitation for this type of physiological time series.

---

## Limitations

- The dataset contains placeholder dates from the year 1900, reducing the reliability of calendar-based features.
- Models are trained globally across all patients and may not be optimal for any given individual.
- Insulin dosing and meal intake data were unavailable, both of which are significant determinants of real-world glucose dynamics.

---

## Future Work

Potential directions for extending this research include:

- Exploration of hybrid CNN-GRU architectures and Transformer-based models with attention mechanisms
- Patient-specific modelling using transfer learning for improved personalisation
- Integration of insulin and carbohydrate intake data for clinically richer predictions
- Deployment of the forecasting model within a real-time CGM application

---

## Technology Stack

Python, TensorFlow, Keras, NumPy, Pandas, Scikit-learn, Matplotlib, Seaborn, Statsmodels

---

## Acknowledgements

Dataset: GlucoBench by IrinaStatsLab.
