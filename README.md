# Ocean Health Monitoring — NOAA World Ocean Database

Machine learning on the NOAA World Ocean Database (WOD) to **predict dissolved oxygen** — a key indicator of water quality — and to **uncover natural structure** in global ocean measurements. Built for SIADS 696 (Milestone 2) by a three-person team.

## Key Findings

Built from a preprocessed dataset of **602,900 global ocean records (2000–2018)** across 17 variables and 23,472 unique locations.

### Predicting dissolved oxygen (supervised)

Four model families were trained to predict dissolved oxygen (μmol/kg) from physical, chemical, and spatio-temporal features, evaluated on a held-out 20% test set (120,580 samples):

| Model | Test RMSE (μmol/kg) | Test R² |
|---|---|---|
| Linear Regression | 56.72 | 0.708 |
| Ridge Regression | 56.74 | 0.708 |
| Neural Network (MLP) | 33.08 | 0.901 |
| Gradient Boosting | 30.25 | 0.917 |
| **Random Forest** | **14.68** | **0.980** |

- **Random Forest was the best model**, explaining ~98% of the variance in dissolved oxygen — a 74% lower test RMSE than linear regression, at the cost of ~100× longer training time. GridSearch tuning further reduced its test RMSE to **14.48**.
- **Top predictors** (Random Forest feature importance): **Phosphate (49.6%)**, Salinity (12.8%), and Latitude (12.3%).
- **Ablation exposed nuance the importance scores miss**: removing Month worsened RMSE by 16% (temporal signal matters despite low ranking), and the model's heavy reliance on Phosphate makes it brittle to sensor failure.
- **Failure analysis** surfaced three distinct error modes: depth-dependent nutrient–oxygen relationships the model flattened (oxygen-minimum zones), geographic bias from sparse Arctic sampling, and ~1.12% of records violating physical oxygen-saturation limits (traced to a single 2005 sensor campaign).

### Discovering ocean regimes (unsupervised)

Four clustering algorithms were compared on the geographic, chemical, and physical features, scored by silhouette:

| Method | Clusters | Silhouette | Notes |
|---|---|---|---|
| **MiniBatch K-Means** | 10 | **0.326** | full dataset |
| Agglomerative (Ward) | 10 | 0.300 | 10% sample |
| DBSCAN | 2 | 0.195 | 36.4% of points labeled noise |
| HDBSCAN | 3 | 0.130–0.195 | 14.1% of points labeled noise |

- **MiniBatch K-Means (k=10) produced the most coherent clusters** and was the only method that scaled to the full 600k-record dataset; agglomerative clustering on a 10% sample agreed closely, a reassuring check on stability.
- Silhouette scores near 0.3 indicate **mild but real structure** — ocean measurements do not fall into sharply separated groups.
- **Salinity, latitude, and oxygen were the most discriminating features** across clusters (bottom depth, pressure, and temperature the least).
- Mapped geographically, clusters form **latitudinal bands of water masses** (consistent with prior oceanographic clustering work) — yet the same cluster appearing in distant oceans shows that chemical/physical composition, not just location, drives the grouping.

Full methodology, figures, and discussion are in [`Results/Ocean_Health_Monitoring_Report.pdf`](Results/Ocean_Health_Monitoring_Report.pdf).

## My Contributions

My primary responsibility was the **unsupervised learning task**, with shared work on data preparation and the report. Specifically, I owned:

- **Unsupervised learning** ([`Unsupervised_Learning.ipynb`](Notebooks/Unsupervised_Learning.ipynb)) — the clustering pipeline end to end: feature selection and scaling, four clustering algorithms (MiniBatch K-Means, Agglomerative, DBSCAN, HDBSCAN) with grid-searched hyperparameters, silhouette-based model selection, PCA/t-SNE visual comparison, effect-size cluster profiling, and the geographic and 3-D spatial visualizations.
- **Data ingestion & formatting** — parsing the raw NOAA WOD export into a standard, analysis-ready table (shared data-prep work in [`Data_Preparation.ipynb`](Notebooks/Data_Preparation.ipynb)).
- **Background research** into the oceanographic context and related work.
- **Report** — authored the introduction, related-works, and unsupervised-learning sections plus the unsupervised discussion, and did final formatting and editing.

The supervised regression/ensemble models (Natasha Soldin) and the neural-network models (Seungdo Woo) were led by my teammates.

## Notebooks

Run in order — each contains inline analysis and rendered outputs.

1. **[Data_Preparation.ipynb](Notebooks/Data_Preparation.ipynb)** — ingest NOAA WOD Ocean Station Data, clean, handle missing values, and run EDA and correlation analysis.
2. **[Supervised_Learning_Task_Part1.ipynb](Notebooks/Supervised_Learning_Task_Part1.ipynb)** — regression and ensembles (Linear, Ridge, Random Forest, Gradient Boosting) for oxygen prediction, with feature importance, ablation, hyperparameter tuning, and failure testing.
3. **[Supervised_Learning_Task_Part2.ipynb](Notebooks/Supervised_Learning_Task_Part2.ipynb)** — a neural-network (MLP) approach and comparison against the classical models.
4. **[Unsupervised_Learning.ipynb](Notebooks/Unsupervised_Learning.ipynb)** — clustering, PCA/t-SNE visualization, cluster profiling, and spatial exploration.

## Data

NOAA **World Ocean Database (WOD)**, Ocean Station Data (OSD) subset, 2000–2018 (accessed September 2025). The data is public and **not tracked in git** due to size — download it into a `Data/` directory via [WODselect](https://www.ncei.noaa.gov/access/world-ocean-database-select/dbsearch.html): select the **Ocean Station Data (OSD)** dataset and your date range, then download as **CSV (observed-level data, with WOD flags, no corrections)**.

> Mishonov A.V., et al. (2024): *World Ocean Database 2023.* NOAA National Centers for Environmental Information. https://doi.org/10.25921/wbve-a685

## Setup

```bash
git clone https://github.com/Auston-B/Ocean-Health-Monitoring.git
cd Ocean-Health-Monitoring
python -m venv venv && source venv/bin/activate   # Windows: venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

Requires Python 3.8+. Download the data (see above), then run the notebooks in order starting with `Data_Preparation.ipynb`.

## Team & License

Natasha Soldin, Auston Balwinski, Seungdo Woo — SIADS 696, University of Michigan School of Information. Data courtesy of NOAA National Centers for Environmental Information. Licensed under the [MIT License](LICENSE).
