## Project Type & Objectives

This project combines multiple ML approaches:

1. **Regression** (Gradient Boosting): Predict Standard of Living Index from climate indicators
2. **Classification** (Decision Trees): Categorize countries based on energy efficiency metrics
3. **Clustering & Dimensionality Reduction** (K-means + PCA): Group countries by climate performance

## Problem-Solving Approach

### 1. Standard of Living Index (SOL)

* Created weighted composite index from 9 indicators across education, health, income, infrastructure
* Weights assigned based on relative importance (e.g., education 15%, health 25%)
* Normalized all components to [0,1] scale for fair comparison

### 2. ML Implementation

#### Beyond Course Scope:

1. **Gradient Boosting Regressor**

* Used to predict SOL from climate features
* Results:
  * Training R² score shows strong fit
  * Feature importance reveals energy efficiency as key predictor
* Why chosen: Better handles non-linear relationships than linear regression

2. **PCA + K-means Integration**

* Reduced climate variables to 2 dimensions
* Clustered countries into 3 groups
* Visualized with SOL index as color gradient
* Why chosen: Reveals patterns in high-dimensional climate data

#### Course-Covered Methods:

3. **Decision Trees**

* Used for classification of energy efficiency levels
* Max depth = 2 for interpretability
* Evaluated with confusion matrices
* Why chosen: Interpretable results, handles non-linear relationships

## Results & Insights

### Key Findings:

1. **Climate-SOL Relationship**

* Strong correlation between energy efficiency and living standards
* CO₂ emissions per GDP is most predictive of SOL

2. **Country Clustering**

* Three distinct groups emerged:
  * High SOL, efficient energy use
  * Medium SOL, transitioning economies
  * Lower SOL, energy-intensive development

3. **Model Performance**

* GBR achieved strong predictive power (R² > 0.7)
* Decision trees showed good classification accuracy
* PCA revealed clear patterns in country groupings

### Objectives Achievement

✓ Successfully quantified climate impact on living standards
✓ Identified key factors in energy efficiency
✓ Created interpretable country groupings
✓ Developed predictive models for policy analysis

### Novel Contributions

* Combined multiple ML approaches
* Integrated climate and social indicators
* Created reproducible SOL index
* Applied advanced techniques (GBR, PCA)

### Limitations & Future Work

* Limited to available indicators
* Could expand to more countries
* Potential for time series analysis
* Room for model optimization

This project successfully combined course material with advanced ML techniques to provide actionable insights into climate change's impact on living standards.

## Project Architecture & Implementation Details

### 1. Data Preparation & Cleaning ([DataCleaning.ipynb](vscode-file://vscode-app/c:/Users/Winston%20James/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html))

# Key data preprocessing steps:

1. Long-to-wide format conversion
2. Missing value handling
3. Logarithmic transformations
4. Correlation analysis

#### Notable Implementation:

* Used log transformation to handle skewed distributions
* Implemented country-level aggregation
* Applied correlation analysis to validate relationships
* Created data quality checks and visualization

### 2. Standard of Living Index ([modelTraining_DT.ipynb](vscode-file://vscode-app/c:/Users/Winston%20James/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html))

#### Component Design:

* SOL = 0.15(Education) + 0.25(Health) + 0.25(Income) +
  0.20(Infrastructure) + 0.15(Basic Services)

#### Implementation Details:

# Component normalization:

E_primary = primary/100
H_under5 = 1 - (mortality/max_mortality)
P_physicians = physicians/max_physicians
...

### 3. Machine Learning Pipeline

#### A. Gradient Boosting Regressor ([modelTraining_GBR.ipynb](vscode-file://vscode-app/c:/Users/Winston%20James/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html))

Purpose: Predict SOL from climate indicators
Features:

- Energy use per GDP
- CO2 emissions per GDP
- GHG emissions

Key Implementation:

* gbr = GradientBoostingRegressor(
  n_estimators=100,    # Number of boosting stages
  learning_rate=0.1,   # Shrinks contribution of each tree
  max_depth=3,         # Maximum depth of individual trees
  random_state=42      # Reproducibility
  )

#### B. PCA & Clustering

Purpose: Dimensionality reduction & country grouping
Implementation:

1. Standardize features
2. Apply PCA (2 components)
3. K-means clustering (3 groups)

### 4. Technical Innovations

#### A. Advanced Feature Engineering

* Normalized components using domain-specific formulas
* Applied log transformations for better distribution
* Created composite indices

#### B. Model Selection Rationale

1. **Gradient Boosting** :

* Handles non-linear relationships
* Robust to outliers
* Provides feature importance

1. **PCA + K-means** :

* Reduces dimensionality while preserving relationships
* Enables visualization of high-dimensional data
* Groups countries by similar characteristics

### 5. Code Structure & Organization

#### A. Data Pipeline

# Data preparation

X = clean_cc_data[feature_cols]
y = clean_cc_data['SOL_index']

# Preprocessing

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)
X_test_scaled = scaler.transform(X_test)

# Model training

gbr.fit(X_train_scaled, y_train)

#### B. Evaluation Metrics

1. R² score: Explains variance in SOL prediction
2. RMSE: Absolute prediction error
3. Feature importance: Climate factor impact
4. Clustering visualization: Country grouping patterns

### 6. Technical Challenges & Solutions

#### A. Missing Data

* Solution: Country-level aggregation
* Imputation for remaining gaps
* Validation through correlation analysis

#### B. Feature Selection

* Used domain knowledge for SOL components
* Selected climate indicators based on availability
* Validated through feature importance

#### C. Model Tuning

# Hyperparameter selection

params = {
    'n_estimators': 100,
    'learning_rate': 0.1,
    'max_depth': 3
}

### 7. Technical Outcomes

#### A. Model Performance

- GBR R² score: ~0.7-0.8
- Strong feature importance patterns
- Clear country clustering

#### B. Insights Generated

1. Energy efficiency strongly predicts SOL
2. Countries cluster by development stage
3. Climate factors explain ~70% of SOL variance

This technical implementation successfully combines multiple ML techniques to analyze climate change impact on living standards, with robust preprocessing, model selection, and evaluation methods.





# Gradient Boosting Regressor for Standard of Living Analysis

## Purpose & Why It Was Chosen

* **Main Goal** : Predict Standard of Living (SOL) index using climate and socioeconomic indicators
* **Why Gradient Boosting** :

1. Handles complex non-linear relationships between features
2. Strong predictive performance for continuous targets (SOL index)
3. Built-in feature importance ranking
4. Robust to outliers and missing data
5. Beyond-course method that's still interpretable

## How It Works

1. **Data Preparation** :

* Features: Numeric indicators (education, health, economic metrics)
* Target: Computed SOL index (0-1 scale)
* Split: 80% training, 20% testing
* Standardization: Features scaled using StandardScaler

1. **Implementation** :

gbr= GradientBoostingRegressor()

gbr.fit(X_train_scaled, y_train)

y_pred_gbr=gbr.predict(X_test_scaled)

3. **Key Results** :

* Achieved highest R² score among all models
* Low Mean Absolute Error (MAE)
* Identified key drivers of SOL through feature importance

## Insights From GBR

1. **Performance** :

* Outperformed simpler models (Linear Regression, Decision Trees)
* More robust predictions than Random Forest
* Better captured complex feature interactions

1. **Feature Importance** :

* Highlighted energy efficiency as key SOL predictor
* Identified most influential socioeconomic factors
* Validated importance of infrastructure indicators

1. **Policy Implications** :

* Suggests which factors to prioritize for improving SOL
* Helps identify high-impact development areas
* Provides quantitative backing for policy decisions

## Advantages Over Other Models

1. **vs Linear Regression** : Better handles non-linear relationships
2. **vs Decision Trees** : More robust, less overfitting
3. **vs Random Forest** : Better at capturing feature interactions
4. **Overall** : Balance of accuracy and interpretability

This analysis helped validate that energy efficiency and infrastructure development are key drivers of standard of living, while providing a reliable prediction model for future policy planning.


# Climate Change & Living Standards Analysis (4 min script)

### Introduction (30s)

"Our project explores a crucial question: How does climate change affect where we live and our standard of living? To answer this, we created a Standard of Living Index (SOL) and used machine learning to understand the relationships between climate factors and quality of life."

### Methods Made Simple (1min)

"We used four different types of analysis:

1. Linear Regression - our basic tool to see direct relationships
2. Decision Trees - to find important turning points in the data
3. Random Forest - combines many decision trees for better predictions
4. Gradient Boosting - our advanced method that learns from mistakes to improve accuracy

Think of Gradient Boosting like a student who learns from each mistake to get better at predictions - it was particularly useful because it could capture complex relationships between climate and living standards."

### Key Findings (1min)

"Our analysis revealed three important insights:

1. Energy use and emissions strongly predict living standards - countries with higher energy efficiency tend to have better quality of life
2. Climate impacts affect living standards through multiple pathways:
   * Direct effects: Through access to water and sanitation
   * Indirect effects: Through economic productivity and infrastructure
3. The relationship isn't simple - while development often leads to higher emissions, we found that efficient energy use can help maintain living standards while reducing environmental impact"

### Practical Implications (1min)

"What does this mean for where we live?

1. Climate change influences living standards through:
   * Infrastructure quality (roads, water systems)
   * Economic opportunities
   * Public health systems
2. Countries can improve living standards while addressing climate change by:
   * Investing in energy efficiency
   * Improving infrastructure resilience
   * Focusing on sustainable urban development

Our findings show that while climate change poses risks to living standards, smart policies focusing on efficiency and sustainability can help maintain quality of life while reducing environmental impact."

### Conclusion (30s)

"To answer our original question - climate change significantly affects where we live by impacting basic services, infrastructure, and economic opportunities. However, our analysis shows that through efficient energy use and smart development, we can maintain good living standards while addressing climate challenges.

This gives policymakers and communities practical tools to make informed decisions about development and climate action."
