# SnowFLOWS  
### Satellite-Based Snow Cover Segmentation and Time-Series Prediction Using Sentinel-2 and Deep Learning

SnowFLOWS is a computer vision and deep learning project for monitoring and forecasting snow cover over Lebanon using Sentinel-2 satellite imagery, Google Earth Engine, and LSTM-based temporal prediction models.

The project combines:
- Remote sensing
- Computer vision (snow segmentation)
- Time-series forecasting
- Deep learning

---

# Project Overview

The pipeline performs:

1. Satellite image acquisition using Sentinel-2 imagery from Google Earth Engine  
2. Snow segmentation using the Normalized Difference Snow Index (NDSI)  
3. Snow area extraction and weekly aggregation  
4. Dataset preprocessing and feature engineering  
5. LSTM-based snow prediction  

---

# Features

- Sentinel-2 preprocessing with cloud masking
- Snow segmentation using NDSI thresholding
- RGB image and snow mask export
- Weekly snow coverage computation
- Time-series dataset construction
- Sequence generation for LSTM
- Multi-feature prediction pipeline
- Sequence length comparison experiments
- Visualization of predictions and loss curves

---

# Project Structure

```text
FYP_1/
│
├── data/
│   ├── masks/
│   └── rgb/
│
├── evaluation/
│   └── evaluate_segmentation.py
│
├── GEE/
│
├── create_sequences.py
├── create_sequences_altitudes.py
├── data_fix_year_representation.py
├── splitting_data.py
├── target_column_added.py
├── zscore_transformation.py
│
├── train_lstm.py
├── train_lstm_altitudes.py
│
├── sequence_comparison.py
├── sequence_comparison.html
│
├── full_timeline_predictions.html
├── full_timeline_predictions_altitudes.html
├── loss_plot.html
├── mae_plot.html
│
├── weekly_snow_model_ready_fixed_dates.csv
├── weekly_snow_model_ready_with_target.csv
│
├── X_train.npy
├── X_val.npy
├── X_test.npy
├── y_train.npy
├── y_val.npy
├── y_test.npy
│
└── README.md
```

---

# Dataset

## Satellite Data
- Source: Sentinel-2 Surface Reflectance
- Platform: Google Earth Engine
- Region: Lebanon
- Temporal coverage: 2016–2025
- Spatial resolution: 10–20 m

## Spectral Bands Used

| Band | Description |
|------|-------------|
| B3 | Green |
| B4 | Red |
| B8 | Near Infrared (NIR) |
| B11 | Short-Wave Infrared (SWIR) |

---

# Snow Segmentation

Snow segmentation is performed using the Normalized Difference Snow Index (NDSI):

```math
NDSI = (Green - SWIR) / (Green + SWIR)
```

Decision rule:

```text
NDSI > 0.4  → Snow
NDSI ≤ 0.4  → Non-snow
```

Output:
- Binary snow masks
- Snow-covered area estimation
- Weekly time-series data

---

# Machine Learning Pipeline

The prediction stage includes:
- Feature engineering
- Z-score normalization
- Sliding-window sequence generation
- LSTM neural networks

Input sequence experiments:
- 1 to 12 weeks
- Best trade-off observed around 6–8 weeks

Evaluation metrics:
- MAE
- RMSE
- IoU
- Dice coefficient
- Pixel accuracy

---

# Installation

## 1. Clone Repository

```bash
git clone https://github.com/ReinaTaher/computer-vision-snowflows.git
cd computer-vision-snowflows
```

---

## 2. Create Environment

```bash
conda create -n snowflows python=3.10
conda activate snowflows
```

---

## 3. Install Dependencies

```bash
pip install numpy pandas matplotlib scikit-learn tensorflow rasterio earthengine-api
```

---

# Running the Project

## 1. Prepare Dataset

```bash
python target_column_added.py
python zscore_transformation.py
python create_sequences.py
```

---

## 2. Train LSTM Model

```bash
python train_lstm.py
```

Alternative altitude-aware model:

```bash
python train_lstm_altitudes.py
```

---

## 3. Run Segmentation Evaluation

```bash
cd evaluation
python evaluate_segmentation.py
```

---

# Running Inference

To generate snow predictions:

```bash
python train_lstm.py
```

The script outputs:
- Predicted snow values
- MAE / RMSE metrics
- Timeline prediction plots
- Loss curves

Generated visualizations:
- `full_timeline_predictions.html`
- `loss_plot.html`
- `mae_plot.html`

---

# Reproducing Computer Vision Pipeline (Snow Segmentation)

The snow segmentation pipeline is implemented in Google Earth Engine (GEE).

## 1. Run Google Earth Engine Script
Open the following script in GEE Code Editor:

```
GEE/snowflows_s2_segmentation.js
```

## 2. Generate Satellite Dataset
The script performs:
- Sentinel-2 image filtering over Lebanon
- Cloud masking using SCL layer
- Computation of NDSI index
- Snow classification using threshold (NDSI > 0.4)

## 3. Export Outputs
From GEE, export:
- RGB images (B4, B3, B2)
- Binary snow masks
- Weekly snow coverage statistics (CSV)

Exported files are saved to Google Drive folder:
```
SnowCV/
```

## 4. Use Outputs in Python Pipeline
The exported CSV and images are used as input for:
- feature engineering
- sequence generation
- LSTM training

---

# Results

## Segmentation Performance
- IoU ≈ 0.74
- Dice ≈ 0.82
- Accuracy ≈ 0.88

## Forecasting Observations
- Short sequences → unstable predictions
- Medium sequences → best trade-off
- Long sequences → smoother but less reactive

---

# Future Improvements

- Deep learning segmentation (U-Net)
- Better cloud handling
- Transformer-based forecasting
- Larger manually labeled datasets
- Real-time monitoring pipeline

---

# Authors

- Reina Taher  
- Carla Youness  
- Nour el Saghir  

### Saint Joseph University of Beirut (USJ)  
### École Supérieure d’Ingénieurs de Beyrouth (ESIB)

---

# License

This project was developed for academic and research purposes.
