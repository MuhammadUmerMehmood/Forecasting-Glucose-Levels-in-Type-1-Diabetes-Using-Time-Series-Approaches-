# Glucose Level Forecasting
This project uses deep learning models (LSTM, GRU, CNN) to predict glucose levels from Continuous Glucose Monitoring (CGM) data.
It’s designed as a Jupyter notebook so you can explore the data, train models, and see results interactively.

# 📂 Project Layout
```
.
├── glucose_forecasting_models.ipynb  # Main notebook
├── data/
│   └── dataset.zip                   # Dataset (zipped for storage)
├── requirements.txt                  # List of dependencies
└── README.md
```

## 🚀 How to Get Started

1. **Clone this repo**
```bash
git clone https://github.com/your-username/glucose-forecasting.git
cd glucose-forecasting
```

2. **Install required libraries**

   - All dependencies are listed in `requirements.txt`.
   - Install them with:
```bash
pip install -r requirements.txt
```

3. **Unzip the dataset**

   - Inside the `data/` folder there is a file `dataset.zip`.
   - Before running the notebook, unzip it:
```bash
unzip data/dataset.zip -d data/
```

#4.Run the notebook

jupyter notebook glucose_forecasting_models.ipynb

#📝 Notes
If you’re using Google Colab, upload the extracted data/ folder before running the notebook.
The notebook includes model training, evaluation, and visualization steps.

#🤖 Models You’ll Find Here
LSTM — learns long-term dependencies in glucose sequences.
GRU — simpler and faster than LSTM but still strong for time series.
CNN — captures short-term glucose spikes and rapid changes.
Each model is compared so you can see which one works best for short-term glucose forecasting.

