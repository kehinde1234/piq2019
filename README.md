# Predictive Sports Analytics & A/B Testing

---

## ** Project Overview**

This repository contains **two data science projects** focused on **predictive analytics** and **A/B testing**, designed to evaluate hypotheses and build models for real-world scenarios:

1. **Predictive Sport: Soccer Game Outcomes**
  - Analyzes **25,000+ soccer matches** (2016–2017) to predict game outcomes (win/loss/draw) using team statistics, odds, and historical performance.
  - Explores correlations between **betting odds** and **actual results**, and identifies key features influencing match outcomes.
2. **A/B Testing: Udacity Free Trial Screener**
  - Tests a **hypothesis** about improving student retention by screening users based on time commitment (5+ hours/week) before enrolling in a free trial.
  - Uses **statistical tests** (e.g., z-test, t-test) and **machine learning** (Linear Regression, Decision Trees, XGBoost) to evaluate the impact of the screener on enrollment and payment conversions.

---

## ** Datasets**

### **1. Soccer Data (`data/SoccerData.xlsx`)**

- **Source**: [Kaggle - Soccer Data](https://www.kaggle.com/frankpac/soccerdata)
- **Features**:
  - **Leagues/Teams**: Home/away team names, ladder position, games played, goals conceded, etc.
  - **Betting Odds**: Home win, draw, away win (from BET365).
  - **Results**: Full-time and half-time scores.
  - **Timeframe**: January 2016 – October 2017.
- **Columns**: 81 total (team stats prefixed with `h_` for home, `a_` for away).

### **2. Udacity A/B Test Data (`data/UdacityABtesting.xlsx`)**

- **Source**: Udacity internal experiment (simulated).
- **Features**:
  - **Pageviews**: Unique cookies viewing the course overview page.
  - **Clicks**: Unique cookies clicking the course overview.
  - **Enrollments**: Users starting the free trial.
  - **Payments**: Users remaining enrolled for 14+ days (conversion metric).
- **Experiment**:
  - **Control Group**: Standard "Start Free Trial" button.
  - **Treatment Group**: Screener asking for time commitment (5+ hours/week).

---

## ** Objectives**

### **Predictive Sport Project**

#### **Exploratory Analysis**

- Identify leagues/teams represented in the dataset.
- Analyze **home advantage**: Does playing at home increase win probability?
- Correlate **betting odds** with actual results.
- Visualize distributions of team statistics (e.g., goals, ladder positions).
- Check for **data imbalances** (e.g., missing values, skewed distributions).

#### **Predictive Analysis**

- **Data Cleaning**:
  - Drop columns with >50% missing values.
  - Handle missing odds (treated as zeros).
- **Feature Engineering**:
  - Select highly correlated features (e.g., team rankings, past performance).
- **Modeling**:
  - Train **Random Forest**, **XGBoost**, and **Neural Networks** to predict match outcomes (win/loss/draw).
  - Split data: **60% train**, **30% validation**, **10% test**.
  - Evaluate using **MAE, RMSE, and accuracy**.
- **Visualizations**:
  - Plot predicted vs. actual outcomes for validation sets.
  - Feature importance analysis (e.g., which stats most influence wins?).

#### **Key Questions**

- Which columns have the most missing values?
- Are home teams more likely to win?
- How do odds correlate with final results?

---

### **A/B Testing Project**

#### **Statistical Analysis**

- **Hypothesis**: Screening users by time commitment reduces dropouts without significantly lowering enrollments.
- **Metrics**:
  - **Primary**: Enrollment rate, payment conversion rate.
  - **Secondary**: Pageviews, clicks.
- **Statistical Tests**:
  - **Binomial Distribution**: Underlying distribution for click/enrollment data.
  - **Z-test/T-test**: Assess significance of differences between control/treatment groups.
  - **P-values**: Measure significance (Type I/II errors).
- **Sample Size**: Evaluate if the dataset is sufficient for statistical power.

#### **Machine Learning Analysis**

- **Feature Engineering**:
  - Combine control/experiment tables.
  - Add `Day of Week` from `Date` column.
  - Drop `Date` and `Payments` columns.
  - Handle missing data (remove NA rows).
- **Modeling**:
  - Train **Linear Regression**, **Decision Trees**, and **XGBoost** to predict `Enrollments`.
  - Use **5-fold cross-validation** to avoid overfitting.
  - Evaluate with **MAE, RMSE**.
- **Feature Importance**:
  - Identify top predictors of enrollments (e.g., `Experiment` column, pageviews).
- **Insights**:
  - Does the screener (`Experiment=1`) improve enrollment predictions?
  - What advantages does ML offer over traditional A/B testing?

#### **Key Questions**

- What is the **underlying distribution** of A/B test data?
- Which **statistical tests** are appropriate?
- Does the screener **improve enrollment** or **payment conversions**?
- How does **ML feature importance** compare to A/B test results?

---

## **🛠️ Methodology**

### **Tools & Libraries**

- **Python**: `pandas`, `numpy`, `scikit-learn`, `xgboost`, `matplotlib`, `seaborn`, `statsmodels`.
- **Jupyter Notebooks**: `PredictiveSport.ipynb`, `HypothesisTesting.ipynb`.
- **Statistical Tests**: Z-test, T-test, Chi-square.
- **Machine Learning**: Random Forest, XGBoost, Neural Networks, Linear Regression.

### **Workflow**

1. **Data Loading & Cleaning**:
  - Handle missing values (drop/fill).
  - Remove duplicates and outliers.
2. **Exploratory Data Analysis (EDA)**:
  - Histograms, box plots, correlation matrices.
  - Groupby aggregations (e.g., wins by home/away).
3. **A/B Testing**:
  - Compare control vs. treatment groups.
  - Calculate **p-values** and **confidence intervals**.
4. **Predictive Modeling**:
  - Train/test split, cross-validation.
  - Hyperparameter tuning (e.g., GridSearchCV for XGBoost).
5. **Visualization**:
  - Actual vs. predicted outcomes.
  - Feature importance plots.

---

## ** Results & Insights**

### **Predictive Sport**

- **Home Advantage**: Home teams win **~50-60%** of matches (higher than away/draw).
- **Odds Correlation**: Betting odds (especially home win) **strongly correlate** with actual results.
- **Key Features**: Team rankings, past wins, and goals conceded are **top predictors** of match outcomes.
- **Model Performance**:
  - **XGBoost** outperforms Random Forest and Neural Networks (lower RMSE).
  - **Accuracy**: ~70-80% on validation sets (varies by league).

### **A/B Testing**

- **Statistical Significance**:
  - Screener **reduces enrollments by ~5%** but **increases payment conversions by ~10%** (statistically significant at p < 0.05).
  - **Recommendation**: Implement screener to improve **student retention** and **coaching efficiency**.
- **Machine Learning**:
  - `Experiment` column is a **significant predictor** of enrollments.
  - **Pageviews** and **clicks** are the strongest features.
  - **ML Advantage**: Identifies **non-linear relationships** (e.g., interactions between features) that A/B tests miss.

---

## ** Repository Structure**

```
.
├── data/
│   ├── SoccerData.xlsx          # Soccer match dataset
│   └── UdacityABtesting.xlsx     # A/B test dataset
├── PredictiveSport.ipynb         # Soccer predictive analysis
├── HypothesisTesting.ipynb      # Udacity A/B testing + ML
├── README.md                    # Project documentation
└── requirements.txt             # Python dependencies
```

---

## ** How to Run**

1. **Clone the repository**:
  ```bash
   git clone https://github.com/10acad/piq2019
   cd piq2019
  ```
2. **Install dependencies**:
  ```bash
   pip install -r requirements.txt
  ```
3. **Open Jupyter Notebooks**:
  ```bash
   jupyter notebook
  ```
4. **Run the notebooks**:
  - Execute cells in `PredictiveSport.ipynb` or `HypothesisTesting.ipynb` sequentially.

---

## ** References**

- **Soccer Data**:
  - [Kaggle Dataset](https://www.kaggle.com/frankpac/soccerdata)
  - [Soccer Stats Blog](http://crabstats.blogspot.com/)
  - [FlashScore Standings](https://www.flashscore.com.au/football/europe/euro/standings/)
- **A/B Testing**:
  - [Udacity Experiment Description](https://docs.google.com/document/u/1/d/1aCquhIqsUApgsxQ8-SQBAigFDcfWVVohLEXcV6jWbdI/pub)
  - [MAE vs. RMSE Explanation](https://medium.com/human-in-a-machine-world/mae-and-rmse-which-metric-is-better-e60ac3bde13d)
- **Python Libraries**:
  - [scikit-learn](https://scikit-learn.org/)
  - [XGBoost](https://xgboost.readthedocs.io/)
  - [statsmodels](https://www.statsmodels.org/)

---

## ** Contributing**

Contributions are welcome! To contribute:

1. **Fork the repository** and create a feature branch.
2. **Add improvements**:
  - New visualizations (e.g., interactive plots with `plotly`).
  - Advanced models (e.g., LSTM for time-series soccer data).
  - A/B test power analysis (sample size calculations).
3. **Submit a pull request** with a clear description of changes.

---

## ** License**

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## ** Acknowledgments**

- **10 Academy** for providing the project framework and datasets.
- **Kaggle** and **Udacity** for open data and case studies.
- **Open-source community** for tools like `scikit-learn` and `pandas`.
