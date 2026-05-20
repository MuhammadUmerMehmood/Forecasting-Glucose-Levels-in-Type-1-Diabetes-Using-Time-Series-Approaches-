# Forecasting Glucose Levels in Type 1 Diabetes Using Machine Learning

**Student:** Muhammad Umer Mehmood · **ID:** 23102319 · **Supervisor:** Ralf Napiwotzki

---

## Overview

This project uses deep learning to forecast blood glucose levels 30 minutes ahead for patients with Type 1 Diabetes. The data comes from Continuous Glucose Monitoring (CGM) devices worn by 200 patients, giving us 647,858 real-world glucose readings to work with.

Three model architectures were built and compared — LSTM, GRU, and CNN — to find out which one best captures the patterns in glucose time series data.

---

## Results

All three models performed well, achieving an R² above 0.94. The GRU came out on top with the lowest error, followed closely by the LSTM, then the CNN.

- GRU: MAE 13.80 mg/dL · RMSE 19.90 · R² 0.9450
- LSTM: MAE 13.96 mg/dL · RMSE 19.96 · R² 0.9447
- CNN: MAE 14.63 mg/dL · RMSE 20.33 · R² 0.9426

---

## Dataset

The dataset is sourced from GlucoBench, a collection of longitudinal CGM records. It covers 200 patients with glucose readings taken every 5 minutes, with values clipped to a clinical range of 40 to 400 mg/dL.

---

## Project Pipeline

The project follows a standard machine learning workflow from raw data through to model evaluation.

The first step was exploratory data analysis — looking at glucose distributions, identifying hypo and hyperglycaemic zones, analysing per-patient variability, and checking for time gaps in the data.

Data preprocessing involved clipping glucose values, engineering lag features, rolling statistics, and rate-of-change features, then normalising and splitting the data into training, validation, and test sets using a 70/15/15 time-based split.

Three models were then trained — LSTM, GRU, and CNN — each with dropout regularisation to prevent overfitting. Training used the Adam optimiser with early stopping to avoid unnecessary epochs.

Finally, all models were evaluated on the test set using MAE, RMSE, and R², with a per-horizon breakdown showing how accuracy changes from 5 to 30 minutes ahead.

---

## Model Architecture

Each model takes 12 timesteps (one hour of history) and 12 features as input, and outputs 6 glucose values representing the next 30 minutes. The LSTM and GRU models use two stacked recurrent layers with dropout, followed by two dense layers. The CNN model uses two convolutional layers with max pooling before the dense layers.

All models were trained with Adam (learning rate 0.001), MSE loss, and early stopping with a patience of 10 epochs over a maximum of 100 epochs.

---

## Features Used

The model uses raw glucose readings alongside engineered features including lagged values from the previous 5, 10, and 15 minutes, rate-of-change over one and two steps, rolling means and standard deviations over 30, 60, and 180 minute windows, and the hour of day to capture daily glucose patterns.

---

## Key Findings

The GRU model proved to be the most effective architecture. Its simpler gating mechanism was sufficient to capture the temporal dynamics of glucose data while being faster to train than the LSTM.

Prediction accuracy was highest in the first 10 to 15 minutes and gradually degraded toward the 30-minute mark, which is expected behaviour for time series forecasting.

The CNN ranked third — it is fast but lacks the sequential memory that recurrent models have, which matters for this type of data.

---

## Limitations

The dataset contains placeholder dates from the year 1900, which limits the reliability of any date-based features. The models are also trained globally across all patients, meaning they may not be optimal for any individual. Insulin dosing and meal data were not available, both of which play a significant role in real-world glucose dynamics.

---

## Future Work

There is room to explore hybrid CNN-GRU architectures and Transformer-based models with attention mechanisms. Patient-specific models using transfer learning could improve personalisation. Integrating insulin and carbohydrate intake data would make the predictions more clinically meaningful, and the eventual goal would be deploying the model into a real-time CGM application.

---

## Tech Stack

Python, TensorFlow, Keras, NumPy, Pandas, Scikit-learn, Matplotlib, Seaborn, Statsmodels

---

Dataset credit: GlucoBench by IrinaStatsLab.
