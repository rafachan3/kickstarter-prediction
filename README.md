# 🚀 Kickstarter Project Success Prediction

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-F7931E?style=flat&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.3-150458?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)](https://jupyter.org/)

A comprehensive machine learning project that predicts Kickstarter crowdfunding campaign success using **supervised learning** (classification) and **unsupervised learning** (clustering) techniques. The analysis uses only features available at project launch, enabling actionable predictions before campaigns begin.

---

## 📊 Key Results

| Model | Metric | Score |
|-------|--------|-------|
| **Random Forest Classifier** | ROC-AUC | **80.05%** |
| **Random Forest Classifier** | Recall | **91.05%** |
| **K-Means Clustering** | Silhouette Score | **0.34** |

### 🎯 Classification Highlights
- Achieved **80% ROC-AUC** on held-out test data (November 2024 projects)
- Identified **funding goal** as the strongest predictor of success (29.5% feature importance)
- Model correctly identifies 91% of successful projects (high recall)

### 🔍 Clustering Insights
- Discovered **6 distinct project segments** with success rates ranging from **24% to 80%**
- Highest success cluster: Low-goal, short-campaign projects (80.1% success rate)
- Lowest success cluster: High-goal ambitious projects averaging $498K (24.1% success rate)

---

## 📁 Dataset

| Attribute | Value |
|-----------|-------|
| **Source** | Kickstarter project data |
| **Time Period** | April 2009 – November 2024 |
| **Total Projects** | 265,019 |
| **Files** | 83 CSV files |
| **Features** | 42 original variables |
| **Classification Subset** | 229,598 projects (successful/failed only) |

---

## 🛠️ Technical Stack

- **Language**: Python 3.12
- **Data Manipulation**: Pandas, NumPy
- **Machine Learning**: scikit-learn
- **Visualization**: Matplotlib, Seaborn
- **Environment**: Jupyter Notebook

---

## 🧠 Methodology

### Part 1: Binary Classification

**Objective**: Predict whether a Kickstarter project will succeed or fail using only launch-time features.

#### Feature Engineering
| Feature | Type | Description |
|---------|------|-------------|
| `log_goal_usd` | Numerical | Log-transformed funding goal in USD |
| `campaign_duration_days` | Numerical | Campaign length (deadline - launch date) |
| `has_video` | Binary | Whether project includes a video presentation |
| `blurb_length` | Numerical | Character count of project description |
| `name_length` | Numerical | Character count of project name |
| `parent_category` | Categorical | Main project category (15 categories) |
| `country` | Categorical | Project country (24 countries) |

#### Model Comparison
| Algorithm | Cross-Validation ROC-AUC |
|-----------|-------------------------|
| Logistic Regression | 0.7567 |
| Decision Tree | 0.7196 |
| **Random Forest** | **0.8257** |

#### Hyperparameter Tuning
- **Method**: GridSearchCV with 5-fold cross-validation
- **Best Parameters**: `n_estimators=150`, `max_depth=20`, `min_samples_split=2`, `min_samples_leaf=1`

#### Train-Test Split Strategy
- **Time-based split** to simulate real-world deployment
- Training: April 2009 – October 2024 (184,204 projects)
- Testing: November 2024 (3,199 projects)

### Part 2: Unsupervised Clustering

**Objective**: Segment Kickstarter projects into meaningful groups to identify distinct archetypes.

#### Clustering Features
- Goal tier (discretized funding goal)
- Funding intensity (goal per campaign day)
- Campaign duration characteristics
- Preparation time (creation to launch)
- Video presence

#### Algorithms Compared
| Algorithm | Clusters | Silhouette Score | Notes |
|-----------|----------|------------------|-------|
| **K-Means** | 6 | 0.3412 | **Selected** - Interpretable, actionable |
| Hierarchical | 2 | 0.5047 | Best separation, limited granularity |
| DBSCAN | 20 | 0.3680 | Many clusters, identifies outliers |

#### Identified Project Segments
| Cluster | Profile | Success Rate | Size |
|---------|---------|--------------|------|
| 1 | Low-Goal, Short-Campaign | **80.1%** | 22,549 |
| 4 | Mid-Goal, Well-Prepared | 77.8% | 49,995 |
| 5 | Micro-Goal | 76.8% | 42,069 |
| 0 | Mid-Goal, Quick-Launch | 62.2% | 72,367 |
| 3 | Mid-Goal, Long-Campaign | 48.5% | 31,708 |
| 2 | High-Goal, Video-Likely | **24.1%** | 10,910 |

---

## 📈 Feature Importance

The Random Forest model identified these as the most predictive features:

```
1. log_goal_usd              29.54%  ████████████████████████████
2. campaign_duration_days    17.66%  █████████████████
3. has_video                 10.82%  ██████████
4. name_length               10.60%  ██████████
5. blurb_length              10.14%  ██████████
6. Category features         14.50%  ██████████████ (combined)
7. Country features           6.50%  ██████ (combined)
```

---

## 💡 Business Insights & Recommendations

Based on the analysis, project creators can improve their success probability by:

1. **Set Realistic Goals** (29.5% importance)
   - Lower funding goals have significantly higher success rates
   - Micro-goal projects (<$1K) achieve 77% success vs. 24% for high-goal projects (>$50K)

2. **Optimize Campaign Duration** (17.7% importance)
   - Short campaigns (<20 days) show the highest success rates (80%)
   - Long campaigns (>45 days) underperform (48.5% success)

3. **Include a Video** (10.8% importance)
   - Projects with videos demonstrate higher success rates
   - Videos signal commitment and help communicate vision

4. **Craft Detailed Descriptions** (20.7% combined)
   - Longer, more descriptive project names and blurbs correlate with success
   - Invest time in clear, compelling copy

---

## 🚀 Getting Started

### Prerequisites
- Python 3.12+
- Conda (recommended) or pip

### Installation

**Option 1: Using Conda (Recommended)**
```bash
# Clone the repository
git clone https://github.com/yourusername/kickstarter-prediction.git
cd kickstarter-prediction

# Create and activate environment
conda env create -f environment.yml
conda activate kickstarter-env
```

**Option 2: Using pip**
```bash
# Clone the repository
git clone https://github.com/yourusername/kickstarter-prediction.git
cd kickstarter-prediction

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

### Running the Analysis
```bash
jupyter notebook kickstarter-prediction.ipynb
```

---

## 📂 Project Structure

```
kickstarter-prediction/
├── README.md                      # Project documentation
├── LICENSE                        # License file
├── environment.yml                # Conda environment specification
├── kickstarter-prediction.ipynb   # Main analysis notebook
├── data/                          # Dataset directory
│   ├── Kickstarter.csv
│   ├── Kickstarter001.csv
│   ├── ...
│   └── Kickstarter082.csv
└── venv/                          # Virtual environment (not tracked)
```

---

## 🔮 Future Improvements

- [ ] **Deep Learning**: Implement neural networks for improved prediction
- [ ] **NLP Analysis**: Apply text analysis to project descriptions using transformers
- [ ] **Time Series**: Analyze temporal trends in crowdfunding success
- [ ] **Web Application**: Build an interactive dashboard for real-time predictions
- [ ] **Feature Engineering**: Extract creator history and previous project success

---

## 📚 Skills Demonstrated

- **Machine Learning**: Classification, clustering, model evaluation, hyperparameter tuning
- **Data Analysis**: Exploratory data analysis, feature engineering, statistical analysis
- **Python Programming**: Pandas, NumPy, scikit-learn, data visualization
- **Data Preprocessing**: Handling missing values, outlier treatment, feature scaling, encoding
- **Model Selection**: Cross-validation, grid search, performance metrics comparison
- **Business Acumen**: Translating technical findings into actionable recommendations

---

## 📄 License

This project is licensed under the terms of the LICENSE file included in this repository.

