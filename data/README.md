# 📂 Data Files

This folder contains both the **processed** and **raw** datasets used in the Nashik Temperature Forecasting project.

---

## 🗃️ Structure

```
├── raw/
│   └── [Hourly Data (Kaggle Source)](https://www.kaggle.com/datasets/parthdande/timeseries-weather-dataset/data)
├── processed/
│   ├── daily_mean.csv
│   └── weekly_avg.csv
└── README.md
```

---

## 🌐 Data Sources

* **Hourly Data (Raw)** — [Download from Kaggle](https://www.kaggle.com/datasets/parthdande/timeseries-weather-dataset/data)
* **daily_mean.csv** — Daily averages of temperature and other weather variables.
* **weekly_avg.csv** — Weekly averages used for time series modeling.

---

## 🧭 Notes

* The raw hourly dataset is hosted externally on **Kaggle** due to its large size.
* The processed CSVs are generated from the Kaggle dataset using preprocessing scripts in the `main` directory.
* All files in the `processed/` folder are ready for direct model training and evaluation.
