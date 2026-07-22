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
│   └── Milestone 2 Report.pdf     # Final report with all results compiled
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

For detailed findings and analysis, please refer to:
- **Project Report**: See `Results/Milestone 2 Report.pdf` for the project final report including methodology, results, discussion and future work recommendations
- **Visualizations**: Run notebooks to obtain exploratory and result visualisations
- **Notebooks**: Each notebook contains inline analysis and interpretations

## Methodology

Our analysis follows a systematic approach:
1. **Data Preprocessing**: Handling missing values, outlier detection, quality control flag analysis, and feature engineering
2. **Exploratory Analysis**: Understanding distributions, correlations, and relationships in ocean variables
3. **Supervised Learning**: Applying regression models to predict oxygen levels and identify key environmental drivers
4. **Deep Learning**: Exploring neural network architectures for complex pattern recognition
5. **Unsupervised Learning**: Discovering natural groupings and reducing dimensionality to understand ocean regimes

## Contributing

This is a university project for SIADS 696. For questions or suggestions, please contact the team members.

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

---

**Note**: This project is for educational purposes as part of the SIADS 696 Milestone 2 assignment.
