# SIADS 696 Milestone 2: Ocean Health Monitoring Using NOAA WOD

A comprehensive machine learning project analyzing ocean health using the NOAA World Ocean Database (WOD). This project applies supervised and unsupervised learning techniques to explore oceanographic patterns, predict dissolved oxygen levels, and uncover hidden structures in ocean data.

## Project Overview

This project utilizes the NOAA World Ocean Database to:
- Apply supervised learning methods to predict ocean oxygen levels and understand key environmental drivers
- Explore oceanographic patterns and relationships through dimensionality reduction and clustering
- Analyze the complex interactions between temperature, salinity, depth, and other ocean variables
- Provide insights into ocean health indicators and environmental patterns across different regions and time periods

## Team Members

- Natasha Soldin
- Auston Balwinski
- Seungdo Woo

## My Contributions

This was a three-person project. My primary responsibility was the **unsupervised learning task**, with shared work on data preparation and the report. Specifically, I owned:

- **Unsupervised learning** ([`Unsupervised_Learning.ipynb`](Notebooks/Unsupervised_Learning.ipynb)) — the clustering pipeline end to end: feature selection and scaling, four clustering algorithms (MiniBatch K-Means, Agglomerative, DBSCAN, HDBSCAN) with grid-searched hyperparameters, silhouette-based model selection, PCA/t-SNE visual comparison, effect-size cluster profiling, and the geographic and 3-D spatial visualizations.
- **Data ingestion & formatting** — parsing the raw NOAA WOD export into a standard, analysis-ready table (shared data-prep work in [`Data_Preparation.ipynb`](Notebooks/Data_Preparation.ipynb)).
- **Background research** into the oceanographic context and related work.
- **Report** — authored the introduction, related-works, and unsupervised-learning sections plus the unsupervised discussion, and did final formatting and editing.

The supervised regression/ensemble models (Natasha Soldin) and the neural-network models (Seungdo Woo) were led by my teammates.

## Repository Structure

```
Ocean-Health-Monitoring/
├── Notebooks/
│   ├── Data_Preparation.ipynb
│   ├── Supervised_Learning_Task_Part1.ipynb
│   ├── Supervised_Learning_Task_Part2.ipynb
│   └── Unsupervised_Learning.ipynb
├── Data/                          # Data extracted from NOAA WOD & processed data produced by Data_Preparation.ipynb (not tracked in git)
├── Results/
│   └── Ocean_Health_Monitoring_Report.pdf   # Final report with all results compiled
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

## Notebooks

### 1. Data Preparation (`Data_Preparation.ipynb`)
- **Data Ingestion**: Loading NOAA WOD Ocean Station Data (OSD)
- **Data Cleaning**: Handling inconsistencies and errors
- **Missing Value Analysis**: Extensive treatment of missing data
- **Exploratory Data Analysis (EDA)**: Statistical summaries and distributions
- **Correlation Analysis**: Understanding relationships between oceanographic variables

### 2. Supervised Learning Part 1 (`Supervised_Learning_Task_Part1.ipynb`)
- **Objective**: Predict dissolved oxygen levels in ocean waters
- **Regression Models**: Linear Regression, Ridge Regression
- **Ensemble Methods**: Random Forest, Gradient Boosting
- **Model Evaluation**: MSE, MAE, R² metrics
- **Feature Importance Analysis**: Identifying key predictors of oxygen levels
- **Ablation Studies**: Testing impact of feature removal
- **Hyperparameter Sensitivity**: GridSearchCV optimization
- **Learning Curves**: Analyzing model performance vs. training size
- **Failure Testing**: Understanding model limitations and edge cases

### 3. Supervised Learning Part 2 (`Supervised_Learning_Task_Part2.ipynb`)
- **Objective**: Apply deep learning approaches to oxygen level prediction
- **Deep Learning Architectures**: Neural network implementations for regression tasks
- **Model Training**: Optimization techniques and convergence analysis
- **Performance Comparison**: Deep learning vs. traditional ML methods
- **Advanced Techniques**: Exploration of complex model architectures

### 4. Unsupervised Learning (`Unsupervised_Learning.ipynb`)
- **Objective**: Discover natural patterns and structures in ocean data without predefined labels
- **Clustering Analysis**: Compare four algorithms to identify ocean regimes — MiniBatch K-Means, Agglomerative (Ward linkage), HDBSCAN, and DBSCAN — with model selection driven by the inertia elbow and silhouette scores
- **Dimensionality Reduction**: PCA and t-SNE projections used to visually compare the resulting cluster assignments in 2-D
- **Cluster Profiling**: Feature effect-size heatmap (per-cluster z-scores vs. the global mean) to characterize what distinguishes each cluster
- **Spatial Exploration**: Geographic mapping of clusters by depth bin and a 3-D latitude × longitude × depth scatter to interpret clusters as ocean regimes

## Data Source

This project uses data from the **NOAA World Ocean Database (WOD)**, specifically the Ocean Station Data (OSD) dataset.

### Data Citation

NOAA World Ocean Database (WOD) was accessed September 2025 from https://www.ncei.noaa.gov/products/world-ocean-database

**Reference:**
> Mishonov A.V., T. P. Boyer, O. K. Baranova, C. N. Bouchard, S. Cross, H. E. Garcia, R. A. Locarnini, C. R. Paver, J. R. Reagan, Z. Wang, D. Seidov, A. I. Grodsky, J. G. Beauchamp, (2024): World Ocean Database 2023. NOAA National Centers for Environmental Information. Dataset. https://doi.org/10.25921/wbve-a685

### How to Obtain the Data

The World Ocean Database is available for public use without restriction. Follow these steps to download the data:

1. **Navigate to WODselect**: Visit [https://www.ncei.noaa.gov/access/world-ocean-database-select/dbsearch.html](https://www.ncei.noaa.gov/access/world-ocean-database-select/dbsearch.html)

2. **Select Criteria**:
   - **Observation Dates**: Choose your date range (e.g., 2000-2018)
   - **Dataset**: Select **Ocean Station Data (OSD)** only
   - **Measured Variables**: 
     - Select variables needed (Temperature, Salinity, Oxygen, etc.)
     - The first checkbox includes the variable if available
     - Leave unselected to include all OSD variables
   - **Optional Filters**: Depth range, country, geographic coordinates, etc.

3. **Generate Query**:
   - Click "Get an Inventory" to preview your selection
   - Review the dataset distribution map and cast count

4. **Download Data**:
   - Click "Download Data"
   - Select **CSV format (standard output)**
   - Choose **Observed level data** (depth measurements in meters)
   - Include **WOD flags** for quality control information
   - Select **No corrections**
   - Provide your email address
   - You'll receive download links via email when the query is complete

5. **Save Data**: 
   - Download the CSV file(s)
   - Place them in the `Data/` directory
   - The files are not tracked in git due to size

**Note**: Query processing time varies based on the amount and complexity of data requested.

## Installation & Setup

### Prerequisites

- Python 3.8+ (check your version with `python --version`)

### Setup Instructions

1. **Clone the repository**:
```bash
git clone https://github.com/Auston-B/Ocean-Health-Monitoring.git
cd Ocean-Health-Monitoring
```

2. **Create a virtual environment** (recommended):
```bash
python -m venv venv

# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

3. **Install dependencies**:
```bash
pip install -r requirements.txt
```

4. **Download the data** following the instructions in the [Data Source](#data-source) section above.

5. **Launch Jupyter Notebook**:
```bash
jupyter notebook
```

6. **Run notebooks in order**: Start with `Data_Preparation.ipynb` and proceed sequentially.

## Dependencies

Key libraries used in this project:
- **Data Processing**: pandas, numpy
- **Visualization**: matplotlib, seaborn, plotly
- **Machine Learning**: scikit-learn
- **Interactive Widgets**: ipywidgets

See `requirements.txt` for the complete list of libraries.

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

## Methodology

Our analysis follows a systematic approach:
1. **Data Preprocessing**: Handling missing values, outlier detection, quality control flag analysis, and feature engineering
2. **Exploratory Analysis**: Understanding distributions, correlations, and relationships in ocean variables
3. **Supervised Learning**: Applying regression models to predict oxygen levels and identify key environmental drivers
4. **Deep Learning**: Exploring neural network architectures for complex pattern recognition
5. **Unsupervised Learning**: Discovering natural groupings and reducing dimensionality to understand ocean regimes

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- NOAA National Centers for Environmental Information for providing the World Ocean Database
- University of Michigan School of Information
- SIADS 696 course instructors and staff

## Contact

For questions about this project, please reach out to:
- nsoldin@umich.edu
- austonb@umich.edu
- seungdo@umich.edu
