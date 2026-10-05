# Universal Machine Learning Engineering Documentation

## 1. Purpose

This document defines a complete and reusable Machine Learning workflow for building reliable, reproducible, and production-ready ML systems.

It covers:

- Data understanding
- Data validation
- Data cleaning
- Exploratory Data Analysis (EDA)
- Data splitting
- Missing-value treatment
- Outlier detection
- Duplicate detection
- Data leakage prevention
- Encoding categorical variables
- Feature engineering
- Feature selection
- Feature scaling
- Dimensionality reduction
- Class imbalance handling
- Model selection
- Baseline modeling
- Hyperparameter optimization
- Model training
- Cross-validation
- Model evaluation
- Error analysis
- Model interpretation
- Final model training
- Model persistence
- Deployment preparation
- Monitoring

The framework supports:

1. Classification
2. Regression
3. Clustering
4. NLP
5. Time Series
6. Tabular Machine Learning
7. Hybrid ML systems

---

# 2. Golden Rule of Machine Learning

A good ML project is not:

```text
Dataset → Model → Accuracy
```

A robust ML project is:

```text
Problem
   ↓
Data Understanding
   ↓
Data Validation
   ↓
Data Cleaning
   ↓
EDA
   ↓
Train/Validation/Test Split
   ↓
Preprocessing
   ↓
Feature Engineering
   ↓
Feature Selection
   ↓
Baseline Model
   ↓
Candidate Models
   ↓
Cross-Validation
   ↓
Hyperparameter Optimization
   ↓
Final Training
   ↓
Evaluation
   ↓
Error Analysis
   ↓
Interpretation
   ↓
Deployment
   ↓
Monitoring
```

The model is only one component of the complete ML system.

---

# 3. Step 1 — Define the ML Problem

Before touching the data, clearly define the problem.

## 3.1 Identify the problem type

### Classification

Predict a discrete category.

Examples:

```text
Spam / Not Spam
Disease / No Disease
Cat / Dog
Fraud / Legitimate
Positive / Negative
```

Possible types:

- Binary classification
- Multiclass classification
- Multilabel classification
- Ordinal classification

---

### Regression

Predict a continuous numerical value.

Examples:

```text
House price
Crop yield
Temperature
Sales
Demand
Revenue
```

---

### Clustering

Discover groups without predefined labels.

Examples:

```text
Customer segmentation
Document grouping
Product grouping
User behavior analysis
```

---

### NLP

Machine learning involving human language.

Examples:

```text
Sentiment analysis
Text classification
Named Entity Recognition
Question answering
Text similarity
Topic classification
Hallucination detection
```

---

### Time Series

Predict or analyze observations ordered by time.

Examples:

```text
Stock prices
Temperature
Sales
Electricity consumption
Traffic
Sensor readings
Crop production
```

---

# 4. Define the Objective

A project should have a measurable objective.

Bad:

```text
Build a disease prediction model.
```

Good:

```text
Build a multiclass disease classification model
that predicts disease categories from patient symptoms
with macro-F1 as the primary evaluation metric.
```

Define:

```text
Input:
    X

Target:
    y

Task:
    Classification / Regression / Clustering / NLP / Time Series

Primary metric:
    F1 / Accuracy / RMSE / MAE / Silhouette Score / etc.

Secondary metrics:
    Precision / Recall / ROC-AUC / R² / etc.

Constraints:
    Model size
    Inference latency
    Memory
    CPU/GPU availability
    Interpretability
```

---

# 5. Data Understanding

Before cleaning anything, understand what the dataset represents.

## 5.1 Inspect dimensions

Determine:

```text
Number of rows
Number of columns
Feature names
Target variable
Data types
```

Questions:

- How many observations exist?
- What does each row represent?
- What does each column represent?
- Which column is the target?
- Which columns are identifiers?
- Which columns contain categorical data?
- Which columns contain numerical data?
- Is there a timestamp?
- Are there text fields?

---

# 6. Data Dictionary

Create a data dictionary.

| Feature | Type        | Description     | Role    |
| ------- | ----------- | --------------- | ------- |
| age     | numerical   | Person age      | Feature |
| gender  | categorical | Gender category | Feature |
| income  | numerical   | Annual income   | Feature |
| disease | categorical | Disease class   | Target  |

Every feature should ideally have:

```text
Name
Data type
Meaning
Units
Allowed values
Missing-value meaning
Source
Feature role
```

---

# 7. Data Validation

Before preprocessing, validate the raw dataset.

Check:

```text
Schema
Data types
Allowed ranges
Missing values
Duplicates
Invalid values
Impossible values
Unexpected categories
Data consistency
Target validity
```

Examples:

```text
Age = -10              → invalid
Temperature = 500°C    → suspicious
Gender = "unknown??"   → inconsistent
Salary = "$50,000"     → wrong representation
Date = "2026/99/99"    → invalid
```

---

# 8. Data Cleaning

Data cleaning should be systematic.

## 8.1 Duplicate Detection

Check for:

- Exact duplicate rows
- Duplicate IDs
- Duplicate observations
- Near-duplicates when appropriate

Never automatically delete duplicates without understanding why they exist.

A duplicate can mean:

```text
Data-entry error
Repeated measurement
Repeated customer
Repeated transaction
Legitimate repeated observation
```

---

# 9. Missing Values

First determine the missingness pattern.

Missing values may be:

```text
NaN
None
NULL
?
Unknown
N/A
-
Empty string
```

Convert inconsistent representations into proper missing values.

## 9.1 Missing-value strategies

### Numerical

Possible methods:

```text
Median
Mean
Constant
Group-wise median
KNN imputation
Iterative imputation
Model-based imputation
```

Median is often safer than mean when the feature is skewed.

---

### Categorical

Possible methods:

```text
Mode
"Unknown"
Most frequent category
Model-based imputation
```

---

### Time Series

Do not blindly use random imputation.

Possible approaches:

```text
Forward fill
Backward fill
Interpolation
Rolling statistics
Domain-specific imputation
```

---

# 10. Outlier Detection

Outliers are observations that significantly differ from the majority.

Methods:

### IQR

```text
Q1 = 25th percentile
Q3 = 75th percentile
IQR = Q3 - Q1

Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
```

### Z-score

Useful when distributions are approximately normal.

### Robust methods

```text
Isolation Forest
Local Outlier Factor
DBSCAN
Robust covariance
```

## Important

Never automatically remove every outlier.

An outlier could represent:

```text
Measurement error
Fraud
Rare disease
Important event
Real extreme behavior
```

Ask:

> Is this observation wrong, or is it simply unusual?

---

# 11. Exploratory Data Analysis

EDA should answer questions about the dataset.

## 11.1 Univariate Analysis

Analyze one feature at a time.

Numerical:

```text
Mean
Median
Std
Variance
Minimum
Maximum
Quantiles
Skewness
Distribution
```

Categorical:

```text
Unique values
Frequency
Percentage
Rare categories
```

Visualizations:

```text
Histogram
KDE
Boxplot
Count plot
```

---

# 12. Bivariate Analysis

Study relationships between two variables.

Examples:

```text
Age vs Income
Temperature vs Yield
Feature vs Target
```

Use:

```text
Scatter plots
Boxplots
Grouped statistics
Correlation
```

For classification:

```text
Feature distribution by class
```

For regression:

```text
Feature vs target relationship
```

---

# 13. Multivariate Analysis

Study multiple variables simultaneously.

Useful techniques:

```text
Correlation matrix
Pair plots
Heatmaps
PCA
Feature interaction analysis
Grouped aggregations
```

Be careful with highly correlated features.

High correlation can indicate:

```text
Redundant information
Multicollinearity
Potential leakage
```

---

# 14. Target Analysis

The target must be analyzed separately.

## Classification

Check:

```text
Class counts
Class percentages
Minority classes
Class imbalance
Label quality
```

Example:

```text
Class A → 70%
Class B → 20%
Class C → 10%
```

Accuracy alone may be misleading.

---

## Regression

Analyze:

```text
Target distribution
Skewness
Outliers
Range
Zero values
Negative values
Long tails
```

Possible transformations:

```text
log1p
Box-Cox
Yeo-Johnson
```

Only apply transformations when justified.

---

# 15. Data Leakage

Data leakage is one of the most serious ML mistakes.

Leakage occurs when information unavailable at prediction time is used during training.

Examples:

```text
Using future information
Using test-set statistics
Scaling before splitting
Feature created using the target
Post-event variables
Duplicate records across train/test
```

Bad:

```text
fit scaler on entire dataset
split dataset
train model
```

Correct:

```text
split dataset

fit scaler on training data

transform training data
transform validation data
transform test data
```

The test set must remain unseen until final evaluation.

---

# 16. Train / Validation / Test Split

Typical structure:

```text
Training      → Model learning
Validation    → Model/model-hyperparameter selection
Test          → Final unbiased evaluation
```

Example:

```text
70% Train
15% Validation
15% Test
```

Or:

```text
80% Train
20% Test
```

with cross-validation inside the training set.

---

# 17. Stratified Splitting

For classification, preserve class proportions when appropriate.

Example:

```text
Original:
Class A = 60%
Class B = 30%
Class C = 10%

Train:
Class A ≈ 60%
Class B ≈ 30%
Class C ≈ 10%
```

Use stratified splitting when the target distribution needs to be preserved.

---

# 18. Time-Aware Splitting

For time-series problems, **never randomly shuffle future and past observations**.

Correct:

```text
Past → Train

Later → Validation

Future → Test
```

Example:

```text
2019–2023 → Train
2024       → Validation
2025       → Test
```

This simulates real-world prediction.

---

# 19. Feature Engineering

Feature engineering transforms raw data into useful representations.

Examples:

```text
Age from date of birth
BMI from height and weight
Total spending
Average transaction value
Day of week
Month
Hour
Interaction terms
Ratios
Rolling statistics
Text embeddings
TF-IDF
```

Good feature engineering can improve a weak model dramatically.

---

# 20. Numerical Features

Numerical features may be:

```text
Continuous
Discrete
Count
Ratio
Ordinal
```

Inspect:

```text
Scale
Distribution
Outliers
Skewness
Zeros
Negative values
```

---

# 21. Categorical Features

Categorical variables may be:

```text
Nominal
Ordinal
Binary
```

Examples:

```text
Gender
Country
Department
Education level
Product category
```

---

# 22. Encoding

## One-Hot Encoding

Best for low-cardinality nominal features.

Example:

```text
Color = Red, Green, Blue
```

becomes:

```text
Color_Red
Color_Green
Color_Blue
```

---

## Ordinal Encoding

Use when categories have meaningful order.

Example:

```text
Low
Medium
High
```

becomes:

```text
0
1
2
```

Do not use ordinal encoding for categories that have no natural order.

---

## Target Encoding

Can be useful for high-cardinality categorical features.

However, it must be implemented carefully to avoid leakage.

Target statistics should be calculated using training data only, preferably using out-of-fold schemes.

---

# 23. Feature Scaling

Scaling is especially important for distance-based and gradient-based algorithms.

## Standardization

```text
z = (x - mean) / standard_deviation
```

Produces approximately:

```text
mean = 0
std = 1
```

Useful for:

```text
Logistic Regression
Linear Regression
SVM
KNN
K-Means
Neural Networks
PCA
```

---

## Min-Max Scaling

Transforms values approximately to:

```text
[0, 1]
```

Useful when bounded feature ranges are desirable.

---

## Robust Scaling

Uses median and IQR.

Useful when strong outliers exist.

---

# 24. Models That Usually Do Not Require Scaling

Tree-based models generally do not require feature scaling.

Examples:

```text
Decision Tree
Random Forest
Extra Trees
Gradient Boosting
XGBoost
LightGBM
CatBoost
```

Scaling them usually does not provide the same benefit it provides to distance-based or linear models.

---

# 25. Feature Selection

Feature selection removes irrelevant, redundant, or harmful features.

Goals:

```text
Reduce dimensionality
Improve generalization
Reduce training time
Reduce overfitting
Improve interpretability
Reduce inference cost
```

---

# 26. Filter Methods

Feature selection independent of a particular model.

Examples:

```text
Variance threshold
Correlation
Chi-square
ANOVA
Mutual information
```

---

# 27. Wrapper Methods

Evaluate subsets of features using a model.

Examples:

```text
RFE
RFECV
Sequential Forward Selection
Sequential Backward Selection
```

More computationally expensive.

---

# 28. Embedded Methods

Feature selection happens during model training.

Examples:

```text
L1 regularization
Lasso
Elastic Net
Tree feature importance
Gradient boosting importance
```

---

# 29. Avoiding Feature Selection Leakage

Do not select features using the entire dataset before cross-validation.

Bad:

```text
Entire dataset
      ↓
Feature selection
      ↓
Cross-validation
```

Better:

```text
Cross-validation
      ↓
Feature selection inside each training fold
      ↓
Model training
      ↓
Validation
```

A preprocessing pipeline should ideally contain:

```text
Imputation
Encoding
Scaling
Feature selection
Model
```

---

# 30. Dimensionality Reduction

When the feature space is large, dimensionality reduction can help.

Methods:

```text
PCA
Truncated SVD
UMAP
Autoencoders
```

PCA is commonly useful for numerical high-dimensional data.

For sparse NLP matrices:

```text
TruncatedSVD
```

is often more appropriate than ordinary PCA.

---

# 31. Class Imbalance

A classification dataset may have:

```text
Class A → 95%
Class B → 5%
```

A model predicting only Class A achieves 95% accuracy while being practically useless for Class B.

Possible solutions:

```text
Class weights
Oversampling
Undersampling
SMOTE
ADASYN
Threshold optimization
Balanced ensemble methods
```

Do oversampling **inside the training folds only**.

Never oversample the test set.

---

# 32. Baseline Model

Always establish a baseline before complex modeling.

Examples:

Classification:

```text
Majority-class classifier
Logistic Regression
Decision Tree
```

Regression:

```text
Mean predictor
Linear Regression
Decision Tree
```

Clustering:

```text
K-Means baseline
```

NLP:

```text
TF-IDF + Logistic Regression
```

Time series:

```text
Naive forecast
Moving average
Seasonal naive
```

The advanced model must beat a meaningful baseline.

---

# 33. Universal Model Selection Strategy

Never select a model simply because it is popular.

Start with:

```text
Problem Type
       ↓
Data Size
       ↓
Feature Type
       ↓
Dimensionality
       ↓
Missing Values
       ↓
Nonlinearity
       ↓
Interpretability
       ↓
Compute Constraints
       ↓
Candidate Models
       ↓
Cross-Validation
       ↓
Metric Comparison
```

---

# 34. Classification Model Selection

Candidate models:

### Linear

```text
Logistic Regression
Linear SVM
```

Good for:

```text
High-dimensional sparse data
NLP
Interpretability
Fast baseline
```

### Tree-based

```text
Decision Tree
Random Forest
Extra Trees
XGBoost
LightGBM
CatBoost
```

Good for:

```text
Tabular data
Nonlinear relationships
Mixed feature interactions
```

### Kernel methods

```text
SVM
```

Useful for:

```text
Small/medium datasets
Nonlinear decision boundaries
```

### Neural Networks

Useful for:

```text
Large datasets
Complex nonlinear patterns
Images
Audio
Text
Sequential data
```

---

# 35. Classification Metrics

## Accuracy

```text
Correct Predictions / Total Predictions
```

Good when classes are reasonably balanced.

---

## Precision

```text
TP / (TP + FP)
```

Answers:

> Of everything predicted positive, how much was actually positive?

---

## Recall

```text
TP / (TP + FN)
```

Answers:

> Of everything actually positive, how much did we detect?

---

## F1 Score

```text
2 × Precision × Recall / (Precision + Recall)
```

Useful when both precision and recall matter.

---

## Macro F1

Calculate F1 independently for each class and average them equally.

Useful for imbalanced multiclass problems.

---

## Weighted F1

Weights each class according to its number of samples.

---

## ROC-AUC

Useful for evaluating ranking/discrimination, particularly binary classification.

---

## PR-AUC

Often more informative than ROC-AUC when positive classes are highly rare.

---

# 36. Classification Evaluation

Always inspect:

```text
Accuracy
Precision
Recall
F1
Confusion Matrix
ROC-AUC where appropriate
PR-AUC where appropriate
Per-class metrics
```

Do not report only accuracy.

For multiclass problems, examine:

```text
Macro F1
Weighted F1
Per-class F1
Confusion matrix
```

---

# 37. Classification Threshold Optimization

Many classifiers produce probabilities.

Example:

```text
P(positive) = 0.73
```

Default threshold:

```text
0.50
```

is not always optimal.

The threshold can be optimized according to:

```text
F1
Recall
Precision
Business cost
False-positive cost
False-negative cost
```

The threshold must be optimized using validation data, not the final test set.

---

# 38. Regression Model Selection

Candidate models:

```text
Linear Regression
Ridge
Lasso
Elastic Net
Decision Tree Regressor
Random Forest Regressor
Extra Trees
Gradient Boosting
XGBoost
LightGBM
CatBoost
SVR
Neural Networks
```

---

# 39. Regression Metrics

## MAE

Mean Absolute Error.

Easy to interpret and relatively robust to extreme errors.

---

## MSE

Mean Squared Error.

Penalizes large errors more heavily.

---

## RMSE

Square root of MSE.

Same units as the target.

---

## R²

Measures explained variance relative to a baseline.

Do not use R² alone.

---

## MAPE

Useful in some business forecasting contexts but problematic when actual values are zero or close to zero.

---

# 40. Regression Error Analysis

Inspect:

```text
Actual vs Predicted
Residuals
Residual distribution
Residual vs prediction
Residual vs feature
Errors by subgroup
Large-error observations
```

A good regression model should not show strong systematic residual patterns.

---

# 41. Clustering

Clustering is unsupervised learning.

There is no target variable.

Common algorithms:

```text
K-Means
MiniBatch K-Means
DBSCAN
HDBSCAN
Agglomerative Clustering
Gaussian Mixture Models
Spectral Clustering
```

---

# 42. K-Means

K-Means attempts to divide observations into K clusters.

Important considerations:

```text
Choose K
Scale features
Handle outliers
Evaluate cluster quality
```

Common K-selection techniques:

```text
Elbow Method
Silhouette Score
Calinski-Harabasz Index
Davies-Bouldin Index
```

---

# 43. Clustering Evaluation

### Silhouette Score

Measures how well each observation fits within its cluster relative to neighboring clusters.

Higher generally indicates better separation.

### Davies-Bouldin

Lower is generally better.

### Calinski-Harabasz

Higher is generally better.

But numerical scores should not replace domain interpretation.

---

# 44. NLP Pipeline

NLP requires a specialized preprocessing workflow.

```text
Raw Text
   ↓
Text Validation
   ↓
Normalization
   ↓
Cleaning
   ↓
Tokenization
   ↓
Representation
   ↓
Feature Engineering
   ↓
Model
   ↓
Evaluation
```

---

# 45. NLP Cleaning

Depending on the task, consider:

```text
Unicode normalization
Whitespace normalization
HTML removal
URL handling
Emoji handling
Punctuation handling
Special-character handling
Language detection
Spelling normalization
Duplicate text detection
```

Do not aggressively remove information.

For example, punctuation and emojis may contain important sentiment information.

---

# 46. Tokenization

Common approaches:

```text
Word tokenization
Subword tokenization
Character tokenization
Sentence tokenization
```

Modern transformer models typically use subword tokenization.

Examples:

```text
BERT
RoBERTa
BanglaBERT
XLM-R
DeBERTa
```

---

# 47. NLP Feature Representation

Traditional:

```text
Bag of Words
TF-IDF
N-grams
```

Neural:

```text
Word embeddings
FastText
Word2Vec
GloVe
```

Transformer:

```text
Contextual embeddings
Transformer hidden states
Fine-tuned language models
```

---

# 48. NLP Model Selection

For small/medium datasets:

```text
TF-IDF + Logistic Regression
TF-IDF + Linear SVM
```

These should often be used as strong baselines.

For larger or complex datasets:

```text
BERT
RoBERTa
DeBERTa
XLM-R
BanglaBERT
Other domain-specific transformers
```

For generative NLP:

```text
Encoder-decoder models
Decoder-only LLMs
Instruction-tuned models
```

---

# 49. NLP Data Leakage

Text datasets frequently contain hidden leakage.

Check for:

```text
Duplicate sentences
Near-duplicate sentences
Same document in train/test
Question-answer pairs from same source
Author leakage
Template leakage
Generated data leakage
```

Near-duplicate detection can be extremely important in NLP benchmarks.

---

# 50. NLP Evaluation

Depends on the task.

Classification:

```text
Accuracy
Precision
Recall
F1
Macro F1
```

NER:

```text
Entity-level precision
Entity-level recall
Entity-level F1
```

Generation:

```text
BLEU
ROUGE
BERTScore
Human evaluation
Task-specific metrics
```

Semantic similarity:

```text
Cosine similarity
Spearman correlation
Pearson correlation
```

---

# 51. Time Series Pipeline

Time series requires special treatment.

```text
Timestamp Validation
       ↓
Sorting
       ↓
Frequency Detection
       ↓
Missing Time Periods
       ↓
Trend Analysis
       ↓
Seasonality Analysis
       ↓
Lag Features
       ↓
Rolling Features
       ↓
Time-Aware Split
       ↓
Model
       ↓
Forecast Evaluation
```

---

# 52. Time Series Validation

Never randomly shuffle chronological data.

Use:

```text
Expanding Window
Rolling Window
Walk-Forward Validation
TimeSeriesSplit
```

Example:

```text
Train: 2019–2021
Valid: 2022

Train: 2019–2022
Valid: 2023

Train: 2019–2023
Test: 2024
```

This better represents production forecasting.

---

# 53. Time-Series Features

Common features:

```text
Lag 1
Lag 7
Lag 14
Lag 30
Rolling mean
Rolling standard deviation
Rolling minimum
Rolling maximum
Difference
Percentage change
Day
Week
Month
Quarter
Year
Day of week
Hour
Holiday indicator
```

For forecasting, every feature must be available at prediction time.

---

# 54. Time-Series Models

Statistical:

```text
ARIMA
SARIMA
Exponential Smoothing
ETS
Prophet
```

Machine Learning:

```text
Random Forest
XGBoost
LightGBM
CatBoost
```

Deep Learning:

```text
LSTM
GRU
Temporal CNN
Transformer-based models
```

The best model depends on the dataset and forecasting horizon.

---

# 55. Time-Series Evaluation

Common metrics:

```text
MAE
RMSE
MAPE
sMAPE
MASE
```

Always compare against a naive baseline.

Example:

```text
Tomorrow's prediction = today's value
```

A complex model that cannot beat a naive forecast is usually not useful.

---

# 56. Cross-Validation

Cross-validation estimates generalization performance.

Typical K-fold:

```text
Fold 1 → Train / Validation
Fold 2 → Train / Validation
Fold 3 → Train / Validation
Fold 4 → Train / Validation
Fold 5 → Train / Validation
```

Final score:

```text
Mean CV Score
+
Standard Deviation
```

---

# 57. Choosing the Correct Cross-Validation

| Problem                          | Recommended CV  |
| -------------------------------- | --------------- |
| Standard classification          | StratifiedKFold |
| Standard regression              | KFold           |
| Grouped data                     | GroupKFold      |
| Time series                      | TimeSeriesSplit |
| Repeated measurements            | Group-aware CV  |
| Highly imbalanced classification | Stratified CV   |

Never blindly use ordinary K-fold for every problem.

---

# 58. Hyperparameter Optimization

Do not manually guess every hyperparameter.

Methods:

```text
Grid Search
Random Search
Bayesian Optimization
Optuna
Successive Halving
Hyperband
```

Random search can be surprisingly effective when only a few hyperparameters strongly affect performance.

---

# 59. Hyperparameter Search Space

Example:

```text
Random Forest:

n_estimators
max_depth
min_samples_split
min_samples_leaf
max_features
class_weight
```

XGBoost:

```text
n_estimators
learning_rate
max_depth
subsample
colsample_bytree
min_child_weight
reg_alpha
reg_lambda
```

Neural Networks:

```text
learning_rate
batch_size
epochs
hidden_size
dropout
weight_decay
optimizer
scheduler
```

---

# 60. Early Stopping

Useful for models where continued training can lead to overfitting.

Concept:

```text
Training performance improves
        ↓
Validation performance improves
        ↓
Validation stops improving
        ↓
Stop training
```

This is especially useful for:

```text
Gradient boosting
Neural networks
Deep learning
```

---

# 61. Model Selection Matrix

A useful starting strategy:

| Data Situation          | Strong Candidates                                  |
| ----------------------- | -------------------------------------------------- |
| Small tabular           | Logistic/Linear, Random Forest, SVM                |
| Medium tabular          | XGBoost, LightGBM, CatBoost, Extra Trees           |
| Large tabular           | LightGBM, XGBoost, CatBoost                        |
| High-dimensional sparse | Linear SVM, Logistic Regression                    |
| NLP classification      | TF-IDF + Linear model, Transformer                 |
| Nonlinear small data    | SVM, Random Forest                                 |
| Clustering              | K-Means, DBSCAN, HDBSCAN                           |
| Time series             | Naive, statistical models, boosting, deep learning |
| Sequential NLP          | Transformer                                        |
| Large complex data      | Deep learning                                      |

This is a **starting point**, not a rule.

---

# 62. Pipeline Design

All transformations should ideally be encapsulated in a reproducible pipeline.

Conceptually:

```text
Input
  ↓
Validation
  ↓
Imputation
  ↓
Encoding
  ↓
Scaling
  ↓
Feature Selection
  ↓
Model
```

This prevents:

```text
Training/validation inconsistency
Data leakage
Manual preprocessing errors
Deployment mismatch
```

---

# 63. Recommended Tabular Pipeline

```text
Raw Dataset
     ↓
Schema Validation
     ↓
Duplicate Handling
     ↓
Invalid Value Handling
     ↓
Train/Test Split
     ↓
Column Detection
     ↓
Numerical Imputation
     ↓
Categorical Imputation
     ↓
Encoding
     ↓
Scaling where required
     ↓
Feature Selection
     ↓
Model
```

---

# 64. Model Training

Training should be reproducible.

Record:

```text
Dataset version
Random seed
Feature list
Preprocessing configuration
Model architecture
Hyperparameters
Library versions
Python version
Training time
Hardware
Metrics
Model version
```

---

# 65. Reproducibility

Set seeds where applicable:

```text
Python
NumPy
Scikit-learn
PyTorch
TensorFlow
```

However, some GPU operations may still have nondeterministic behavior.

Record environment information.

---

# 66. Error Analysis

After evaluation, investigate failures.

Ask:

```text
Which examples fail?
Why do they fail?
Are certain classes harder?
Are certain demographic/geographic groups harder?
Are there mislabeled examples?
Are there outliers?
Is the feature representation insufficient?
Is the model underfitting?
Is the model overfitting?
```

---

# 67. Confusion Matrix Analysis

For classification, identify:

```text
True Positives
True Negatives
False Positives
False Negatives
```

For multiclass:

```text
Which class is confused with which?
```

This often reveals more than overall accuracy.

---

# 68. Overfitting

Signs:

```text
Training score very high
Validation score significantly lower
```

Solutions:

```text
More data
Regularization
Feature selection
Simpler model
Dropout
Early stopping
Data augmentation
Cross-validation
Reduce model complexity
```

---

# 69. Underfitting

Signs:

```text
Training performance poor
Validation performance also poor
```

Solutions:

```text
Better features
More expressive model
Less regularization
Better preprocessing
More training
Reduce excessive feature removal
```

---

# 70. Bias-Variance Tradeoff

High bias:

```text
Model too simple
Underfitting
```

High variance:

```text
Model too complex
Overfitting
```

The goal is to find a model that generalizes well.

---

# 71. Model Interpretability

Depending on the model, use:

```text
Feature importance
Permutation importance
SHAP
Partial dependence
LIME
Coefficients
Attention analysis
Counterfactual analysis
```

Interpretability is especially important in:

```text
Healthcare
Finance
Education
Legal systems
Government
High-risk decisions
```

---

# 72. Final Model Selection

Do not choose the model solely based on the highest validation score.

Consider:

```text
Validation performance
CV mean
CV variance
Test performance
Inference latency
Model size
Memory consumption
Interpretability
Robustness
Maintenance complexity
Deployment requirements
```

A model that is 0.2% better but 20× more expensive may not be the correct production choice.

---

# 73. Final Training

Once the model and pipeline are selected:

```text
Training + validation data
        ↓
Fit final preprocessing
        ↓
Fit final model
        ↓
Keep test data untouched
        ↓
Evaluate once on test set
```

The final test set should ideally be used only for the final unbiased estimate.

---

# 74. Model Serialization

Save the complete inference pipeline.

For traditional Python ML:

```text
joblib
pickle
```

For deep learning:

```text
PyTorch checkpoint
Safetensors
TensorFlow SavedModel
ONNX
```

Prefer saving:

```text
Preprocessing
Feature selection
Model
Label encoder
Metadata
```

as one coherent inference artifact where practical.

---

# 75. Deployment

Possible deployment architecture:

```text
Client
   ↓
REST API
   ↓
Input Validation
   ↓
Preprocessing Pipeline
   ↓
Model
   ↓
Prediction
   ↓
Post-processing
   ↓
JSON Response
```

Common technologies:

```text
FastAPI
Flask
Docker
Kubernetes
Cloud VM
Cloud Run
AWS
Azure
GCP
```

---

# 76. Production Monitoring

After deployment, monitor:

```text
Latency
Throughput
Errors
CPU
Memory
Prediction distribution
Input distribution
Data drift
Concept drift
Model performance
```

---

# 77. Data Drift

Data distribution changes over time.

Example:

```text
Training:
Age average = 30

Production:
Age average = 47
```

Possible drift detection:

```text
PSI
KS test
Distribution comparison
Population statistics
Embedding drift
```

---

# 78. Concept Drift

The relationship between input and target changes.

Example:

```text
X → Y relationship during training

changes later

X → different Y relationship
```

This is especially important for:

```text
Fraud detection
Financial prediction
Recommendation systems
Demand forecasting
Traffic prediction
```

---

# 79. Production Retraining

Retraining should have a defined strategy.

Possible triggers:

```text
Performance degradation
Data drift
Concept drift
New labeled data
Scheduled retraining
Business requirement
```

Version:

```text
Model v1
Model v2
Model v3
```

Never silently replace production models.

---

# 80. Universal ML Checklist

## Problem

- [ ] Problem clearly defined
- [ ] ML task identified
- [ ] Target defined
- [ ] Evaluation metric selected
- [ ] Constraints identified

## Data

- [ ] Dataset source documented
- [ ] Schema inspected
- [ ] Data types checked
- [ ] Target checked
- [ ] Duplicates investigated
- [ ] Missing values investigated
- [ ] Invalid values investigated
- [ ] Outliers investigated

## EDA

- [ ] Numerical distributions
- [ ] Categorical distributions
- [ ] Target distribution
- [ ] Correlation analysis
- [ ] Feature-target relationships
- [ ] Class imbalance
- [ ] Potential leakage

## Splitting

- [ ] Train/test split performed
- [ ] Stratification where appropriate
- [ ] Group separation where required
- [ ] Time-aware split where required
- [ ] Test set isolated

## Preprocessing

- [ ] Missing-value strategy
- [ ] Categorical encoding
- [ ] Numerical scaling
- [ ] Outlier strategy
- [ ] Feature engineering
- [ ] Feature selection
- [ ] Dimensionality reduction if needed

## Modeling

- [ ] Baseline established
- [ ] Multiple candidate models tested
- [ ] Correct CV strategy selected
- [ ] Hyperparameter tuning performed
- [ ] Best model selected based on appropriate metric

## Evaluation

- [ ] Validation metrics
- [ ] Cross-validation metrics
- [ ] Test metrics
- [ ] Confusion matrix where applicable
- [ ] Error analysis
- [ ] Subgroup analysis
- [ ] Overfitting analysis

## Deployment

- [ ] Pipeline serialized
- [ ] Model versioned
- [ ] Environment documented
- [ ] API tested
- [ ] Input validation implemented
- [ ] Monitoring implemented

---

# 81. Recommended Project Structure

```text
ml-project/
│
├── data/
│   ├── raw/
│   ├── interim/
│   ├── processed/
│   └── external/
│
├── notebooks/
│   ├── 01_data_understanding.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_eda.ipynb
│   ├── 04_feature_engineering.ipynb
│   ├── 05_feature_selection.ipynb
│   ├── 06_baseline_models.ipynb
│   ├── 07_model_comparison.ipynb
│   └── 08_error_analysis.ipynb
│
├── src/
│   ├── data/
│   │   ├── validation.py
│   │   ├── cleaning.py
│   │   └── preprocessing.py
│   │
│   ├── features/
│   │   ├── engineering.py
│   │   └── selection.py
│   │
│   ├── models/
│   │   ├── baseline.py
│   │   ├── train.py
│   │   ├── tune.py
│   │   └── evaluate.py
│   │
│   └── utils/
│       ├── config.py
│       ├── logging.py
│       └── reproducibility.py
│
├── models/
│   ├── candidate/
│   └── final/
│
├── reports/
│   ├── figures/
│   ├── metrics/
│   └── experiments/
│
├── tests/
│
├── configs/
│   └── config.yaml
│
├── requirements.txt
├── README.md
└── ML_DOCUMENTATION.md
```

---

# 82. Universal Decision Framework

Use this decision process before selecting a model.

```text
                         START
                           │
                           ▼
                    What is the task?
                           │
       ┌───────────┬───────┼───────────┬─────────────┐
       ▼           ▼       ▼           ▼             ▼
 Classification Regression Clustering  NLP       Time Series
       │           │       │           │             │
       ▼           ▼       ▼           ▼             ▼
 Analyze       Analyze   Scale if   Text        Chronological
 imbalance     target    necessary  pipeline       split
       │           │       │           │             │
       ▼           ▼       ▼           ▼             ▼
 Baselines     Baselines Candidate  TF-IDF /    Naive baseline
       │           │       models    Transformer       │
       ▼           ▼       │           │               ▼
 Candidate     Candidate   │           │          Statistical/
 models         models     │           │             ML/
       │           │       │           │             DL
       └───────────┴───────┴───────────┴──────────────┘
                           │
                           ▼
                   Cross Validation
                           │
                           ▼
                  Hyperparameter Tuning
                           │
                           ▼
                     Error Analysis
                           │
                           ▼
                    Final Model
                           │
                           ▼
                      Deployment
                           │
                           ▼
                      Monitoring
```

---

# 83. The Most Important Rules

## Rule 1

**Never fit preprocessing on the test set.**

---

## Rule 2

**Never perform feature selection using the entire dataset before validation.**

---

## Rule 3

**Never use future information to predict the past.**

---

## Rule 4

**Never judge a model using only training performance.**

---

## Rule 5

**Always establish a baseline.**

---

## Rule 6

**Use the evaluation metric that matches the actual problem.**

---

## Rule 7

**Do not remove outliers blindly.**

---

## Rule 8

**Do not assume scaling is always necessary.**

---

## Rule 9

**Do not assume the most complex model is the best model.**

---

## Rule 10

**Keep the complete preprocessing + model pipeline reproducible.**

---

# 84. Final Universal Workflow

The recommended workflow is:

```text
01. Define Problem
        ↓
02. Understand Dataset
        ↓
03. Validate Schema
        ↓
04. Identify Target
        ↓
05. Inspect Missing Values
        ↓
06. Detect Duplicates
        ↓
07. Detect Invalid Values
        ↓
08. Analyze Outliers
        ↓
09. Perform EDA
        ↓
10. Identify Leakage
        ↓
11. Split Data
        ↓
12. Build Preprocessing Pipeline
        ↓
13. Handle Missing Values
        ↓
14. Encode Categorical Variables
        ↓
15. Engineer Features
        ↓
16. Scale Features When Appropriate
        ↓
17. Select Features
        ↓
18. Establish Baseline
        ↓
19. Select Candidate Models
        ↓
20. Cross-Validate
        ↓
21. Tune Hyperparameters
        ↓
22. Compare Models
        ↓
23. Perform Error Analysis
        ↓
24. Select Final Model
        ↓
25. Train Final Pipeline
        ↓
26. Evaluate on Unseen Test Set
        ↓
27. Interpret Model
        ↓
28. Save Model
        ↓
29. Deploy
        ↓
30. Monitor
        ↓
31. Retrain When Necessary
```

# 85. Definition of a "Good" ML System

A good ML system is not necessarily the system with the highest score.

A strong ML system should be:

```text
Accurate
+
Generalizable
+
Leakage-free
+
Reproducible
+
Robust
+
Interpretable when required
+
Computationally practical
+
Maintainable
+
Deployable
```

The final objective is:

> **Build the simplest model that reliably solves the real-world problem under the actual constraints.**
