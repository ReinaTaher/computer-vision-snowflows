# SnowFLOWS – Snow Segmentation and Time-Series Prediction from Satellite Imagery

## Project Overview

SnowFLOWS is a computer vision and machine learning project that analyzes and predicts snow coverage evolution using satellite imagery.

The project combines:
- Google Earth Engine (GEE) for satellite data extraction
- Computer Vision for snow segmentation using NDSI
- Machine Learning (LSTM) for time-series forecasting of snow coverage

The main objective is to estimate and predict snow dynamics over Lebanon using Sentinel-2 imagery.

---

## Project Pipeline

### 1. Satellite Data Acquisition (GEE)
- Sentinel-2 Level-2A imagery is used
- Cloud masking is applied using the SCL band
- Images are filtered spatially over Lebanon and temporally over multiple years

---

### 2. Snow Segmentation (Computer Vision)
Snow detection is performed using the Normalized Difference Snow Index (NDSI):

NDSI = (Green - SWIR) / (Green + SWIR)

Snow pixels are classified using:
- Threshold: NDSI > 0.4

Outputs:
- RGB satellite images
- Binary snow masks (GeoTIFF format)
- Paired datasets for evaluation and machine learning

---

### 3. Dataset Preparation
From segmentation results:
- Snow coverage is extracted per image
- Weekly time-series dataset is constructed
- Features are normalized using Z-score normalization
- Sequences are generated for temporal learning

---

### 4. Time-Series Prediction (LSTM)
LSTM models are trained to predict future snow coverage.

Inputs:
- Historical snow coverage sequences
- Optional altitude-based features

Outputs:
- Future snow coverage prediction

---

## Project Structure


---

## Google Earth Engine (GEE)

- Sentinel-2 Surface Reflectance data is used
- Cloud masking is applied using Scene Classification Layer (SCL)
- Snow detection is performed using NDSI thresholding
- Outputs include:
  - RGB images
  - Binary snow masks
  - Temporal snow coverage estimates

---

## Evaluation (Computer Vision)

Segmentation performance is evaluated using:

- Intersection over Union (IoU)
- Dice Coefficient
- Pixel Accuracy

These metrics measure the similarity between predicted and reference snow masks.

---

## Machine Learning Model (LSTM)

### Input:
- Sequential snow coverage values over time
- Optional altitude-based features

### Output:
- Future snow coverage prediction

### Models:
- Basic LSTM model (`train_lstm.py`)
- Enhanced LSTM with altitude features (`train_lstm_altitudes.py`)

---

## Outputs

The project generates:
- Snow coverage predictions over time
- Loss and MAE training curves
- Interactive visualizations (HTML files)
- Sequence comparison plots

---

## Installation

```bash
pip install numpy pandas tensorflow scikit-learn rasterio matplotlib
