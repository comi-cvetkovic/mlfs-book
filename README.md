# MLFS Lab – Air Quality Forecasting Pipeline  
KTH – Machine Learning Full Stack (MLFS)  
**Student:** Mihailo Cvetković  
**Date:** 18 November 2025  

---

## 📌 Project Overview

This project implements a **full end-to-end Machine Learning system** for *air quality forecasting* using the Hopsworks Feature Store and the MLFS Book framework.  
The goal is to predict daily PM2.5 air pollution levels using:

- historical air quality sensor data (AQICN)
- weather features (Open-Meteo)
- ML model (XGBoost Regressor)
- daily ingestion & monitoring pipelines

The implementation follows the notebook structure from the MLFS Book:

1. **Part 01 – Air Quality Feature Engineering**  
2. **Part 02 – Weather Feature Engineering**  
3. **Part 03 – Training Pipeline**  
4. **Part 04 – Batch Inference & Monitoring**

The full pipeline successfully:

✔ creates feature groups  
✔ performs backfilling  
✔ trains and registers an ML model  
✔ generates hindcast monitoring data  
✔ supports the dashboard visualizations  

---

## 🧱 System Architecture (High-Level)

AQICN API Open-Meteo API
│ │
▼ ▼
Air Quality FG Weather FG
└─────── Feature View ───────┐
▼
Training Pipeline
▼
XGBoost Model
▼
Batch Inference / Monitoring
▼
Dashboard (Hopsworks)


---

## 📂 Repository Structure

Your fork of **mlfs-book** contains all notebooks and source files used in the project.

Key folders:

mlfs-book/
│
├── notebooks/
│ ├── 1_air_quality_feature_backfill.ipynb
│ ├── 2_weather_feature_backfill.ipynb
│ ├── 3_training_pipeline.ipynb
│ ├── 4_batch_inference_monitoring.ipynb
│
├── mlfs/
│ ├── airquality/
│ │ ├── util.py
│ │ ├── metadata.py
│ │ └── (other utility files)
│ └── (framework helper modules)
│
├── history/
│ └── (saved plots, metrics, model outputs)
│
└── README.md ← (this file)


> ⚠️ **Note:** `.env` is intentionally **not included** in the repo for security reasons.

---

## 🚀 How to Run the Project

### 1. Clone your GitHub repo
```bash
git clone https://github.com/<your_username>/mlfs-book
cd mlfs-book

2. Create a .env file
The project requires:

HOPSWORKS_API_KEY=1oipaqJHbbW58upQ.yE4f04v8MQOpddXtkNfMWcdnGU67eBK8Vl1a0uOXwf3rKb2o1bNDzBUrymi88y6O
HOPSWORKS_HOST=c.app.hopsworks.ai
HOPSWORKS_PROJECT=mihailos
AQICN_API_KEY=646929f7726b7a588ce674204df2b130c4bc4f2e
AQICN_URL=https://api.waqi.info/feed/@8093
AQICN_COUNTRY=Serbia    
AQICN_CITY=Belgrade
AQICN_STREET=Mostar

3. Start Jupyter notebook
jupyter notebook

4. Run notebooks in order

1_air_quality_feature_backfill.ipynb

2_weather_feature_backfill.ipynb

3_training_pipeline.ipynb

4_batch_inference_monitoring.ipynb

🏗 Feature Store Components
✔ Air Quality Feature Group

Created from AQICN sensor readings.
Primary keys: city, street, datetime.

✔ Weather Feature Group

Created using Open-Meteo forecast data.
Primary keys: city, street, datetime.

✔ Feature View

Joined weather + air quality into a unified dataset (air_quality_fv).

🤖 Model Training & Registry

Model: XGBoost Regressor

Logged to the Hopsworks Model Registry

Training datasets created (versions 1 → 4)

Metrics such as MAE, RMSE stored in history

📊 Monitoring & Hindcast

The monitoring pipeline:

Loads the latest model from Model Registry

Generates daily predictions

Produces hindcast dataset for previous days

Inserts results into monitoring feature group

Creates plots & PNG files for dashboard

🌐 Dashboard (Public URL)

Hopsworks Project Dashboard: https://c.app.hopsworks.ai/p/1306773/settings/general

This dashboard gives access to:

Feature Groups

Feature Views

Training Datasets

Model Registry

Batch inference / monitoring tables







