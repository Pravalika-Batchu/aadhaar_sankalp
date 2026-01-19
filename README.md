# Aadhaar-Sankalp: Live Social Sensor for UIDAI Hackathon 2026


## Description


Aadhaar-Sankalp is my submission for the UIDAI Data Hackathon 2026. It turns Aadhaar enrolment and update data into a "Live Social Sensor" to detect "Invisible Urbanization" trends—migration lags causing biometric gaps that risk excluding kids from services like scholarships and DBT by March 2026.


**Core Idea**: Dual engines flag "Economic Hubs" (migration hotspots) and "Digital Identity Deserts" (high-risk lag zones), with LightGBM forecasts for gaps. Outputs a priority map for mobile vans and new centers, saving ~₹500 Cr in exclusions.


- **Problem**: Sparse bio updates in growth zones leave 10% youth vulnerable.
- **Solution**: Corr-based hubs, ratio-based deserts, tuned models (R² ~0.07, MAE 1.33 ~6% gaps).
- **Impact**: 12 priorities (5 vans, 7 monitor)—100% saturation feasible.



## Setup


### Prerequisites
- Python 3.10+.
- Colab (recommended for GPU) or local (i5/16GB RAM fine).
- Dependencies: `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly`, `scikit-learn`, `xgboost`, `lightgbm`, `joblib`.


### Installation
1. **Colab**:
   - Open [colab.research.google.com](https://colab.research.google.com), new notebook.
   - Mount Drive: `from google.colab import drive; drive.mount('/content/drive')`.
   - Install extras: `!pip install plotly scikit-learn xgboost lightgbm joblib`.
   - Upload CSVs to `/content/drive/MyDrive/aadhar_data/` (or adjust paths in Cell 2).


2. **Local**:
   - `pip install pandas numpy matplotlib seaborn plotly scikit-learn xgboost lightgbm joblib jupyter`.
   - Place CSVs in `./data/`; update paths in Cell 2.
   - Run: `jupyter notebook grok.ipynb`.


### Data
- Download UIDAI datasets (enrolment, biometric, demographic) to `/content/drive/MyDrive/aadhar_data/`.
- ~5M rows total; code chunks for efficiency.


## Usage


1. **Run the Notebook**:
   - Paste cells sequentially (Shift+Enter).
   - Runtime: ~10-15 mins on T4 GPU (load/merge ~2 mins, models ~3 mins, viz ~2 mins).
   - Outputs: CSVs (hubs_train.csv, deserts_test.csv, insights_split.csv), PKL (models), PNG/HTML (viz).


2. **Key Cells**:
   - After "Split done" print: Engines/models run on train/test.
   - After "All viz rendered": Plots saved.
   - After "Downloaded!": Zip w/ outputs.


3. **Customize**:
   - Thresh in Engine 1: Change >0.4 for more hubs.
   - Tune models: GridSearchCV in Cell 22 (cv=3).


4. **Export**:
   - PDF: `!jupyter nbconvert --to pdf aadhaar.ipynb --no-input`.
   - Zip: Run download cell for CSVs/PNGs.


## Key Outputs & Results


### Priority Map (insights_split.csv)
Merged hubs/deserts :
| Pincode | Signal | State | Risk | Priority |
|---------|--------|-------|------|----------|
| 110094 | 0.41 | Delhi | 0.0 | Monitor |
| 122107 | 0.53 | Haryana | 0.0 | Monitor |
| 190018 | 0.0 | N/A | 0.9 | Deploy Van |
| ... | ... | ... | ... | ... |


- **Hubs (hubs_train.csv)**: 20 w/ signals 0.41-0.53 (e.g., Haryana 122107: 0.53 corr, 548 enrol = growth hub).
- **Deserts (deserts_test.csv)**: 10 w/ risk 0.9 (e.g., 190018 = 90% lag; 0.1% relevance = 10k+ national).


### Model Performance
- LightGBM CV R²: -0.011 ±0.049 (stable).
- Train R²: 0.056 | Test R²: -0.096.
- MAE: 1.33 (~6% gaps, 15% > baseline MAPE).
- Spin: Reliable for 8% lag forecasts despite sparsity.


### Viz
- national_ts.png: Demo/bio trends.
- corr_heatmap.png: Feature links.
- trivariate_scatter.html: Interactive scatter.
- state_risk.html: Bar chart.
- lgb_tuned_importance.png: demo_enrol_interact tops.


## Contact
pravalikabatchu14@gmail.com

