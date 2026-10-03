Yes. Based on the actual project report, research paper, and the results already produced, here is a **complete README.md** you can paste directly into GitHub. I’m not adding random claims that aren't supported by your project.

```markdown
# Corporate Bankruptcy Prediction Using Machine Learning

A machine learning classification project for predicting whether a company is likely to become bankrupt based on financial indicators.

## 📌 Project Overview

Corporate bankruptcy prediction is a binary classification problem in which financial indicators are used to determine whether a company belongs to the bankrupt or non-bankrupt class.

The main objective of this project is to implement and compare multiple machine learning classification algorithms on the Polish Companies Bankruptcy Dataset and study how different models perform on a highly imbalanced dataset.

The project reproduces the major models discussed in the reference research paper and extends the comparison with Random Forest. An additional Balanced Random Forest experiment was performed to investigate the effect of class imbalance.

---

## 🎯 Objectives

The project aims to:

- Predict corporate bankruptcy using financial indicators.
- Implement multiple machine learning classification algorithms.
- Compare the performance of different classifiers using the same dataset and train-test split.
- Evaluate models using accuracy, log loss, precision, recall, F1-score and confusion matrix.
- Perform 5-fold stratified cross-validation.
- Analyze the effect of severe class imbalance on bankruptcy detection.
- Extend the reference-model comparison using Random Forest.
- Investigate whether class weighting with Balanced Random Forest improves minority-class detection.

---

## 📊 Dataset

The project uses the **Polish Companies Bankruptcy Dataset** obtained from the UCI Machine Learning Repository.

The selected dataset is the **third-year forecasting dataset (`3year.arff`)**, containing financial information about Polish companies.

### Dataset Characteristics

| Property | Value |
|---|---:|
| Total companies | 10,503 |
| Financial features | 64 |
| Target classes | 2 |
| Non-bankrupt companies | 10,008 |
| Bankrupt companies | 495 |

The target variable represents whether a company is bankrupt or non-bankrupt.

The dataset is highly imbalanced because the number of non-bankrupt companies is substantially larger than the number of bankrupt companies.

This class imbalance is an important part of the project because a model can achieve high overall accuracy while still performing poorly at detecting bankrupt companies.

---

## 🧹 Data Preprocessing

The ARFF dataset was loaded and converted into a Pandas DataFrame.

The preprocessing workflow consisted of the following steps:

1. Load the dataset.
2. Separate the target variable from the 64 financial features.
3. Handle missing values using mean imputation.
4. Perform an 80:20 stratified train-test split.
5. Use the same train-test split for all models to ensure a consistent comparison.
6. No feature standardization was applied.

### Missing Value Handling

Missing values were handled using **mean imputation**.

The imputer was fitted using the training data and subsequently applied to the test data.

For cross-validation, mean imputation was included inside the cross-validation pipeline to prevent data leakage.

### Train-Test Split

An 80:20 stratified split was used.

```text
Training set: 8,402 instances
Testing set:  2,101 instances
```

The stratification preserves the class distribution between the training and testing datasets.

---

## 🔬 Methodology

The overall workflow of the project is:

```text
Dataset
   ↓
Data Loading
   ↓
Missing Value Handling
   ↓
Mean Imputation
   ↓
Target / Feature Separation
   ↓
80:20 Stratified Train-Test Split
   ↓
Model Training
   ↓
Prediction
   ↓
Evaluation
   ↓
5-Fold Stratified Cross-Validation
   ↓
Model Comparison
   ↓
Class Imbalance Analysis
```

The same train-test split was used for all models so that their performance could be compared fairly.

---

# 🤖 Machine Learning Models

The project implements seven classifiers.

## 1. Logistic Regression

Logistic Regression is a linear classification algorithm that models the probability of a binary outcome using the logistic/sigmoid function.

The reference research paper used L2 regularization to reduce overfitting and control large model weights.

---

## 2. Support Vector Machine (SVM)

Support Vector Machine is a supervised classification algorithm that attempts to find a separating hyperplane with a large margin between classes.

The reference study investigated SVM for bankruptcy prediction and reported strong performance.

---

## 3. Neural Network / MLP

A Neural Network was used as another nonlinear classification approach.

The reference study used a neural network architecture with hidden layers and investigated its ability to predict corporate bankruptcy from financial indicators.

---

## 4. Bernoulli Naive Bayes

Bernoulli Naive Bayes is a probabilistic classifier based on Bayes' theorem and the assumption of conditional independence between features given the class.

The reference research specifically used the Bernoulli Naive Bayes model.

---

## 5. XGBoost

XGBoost is an implementation of gradient boosting designed to build an ensemble of prediction models.

The reference study investigated Extreme Gradient Boosting and used regularization to control overfitting.

---

## 6. LightGBM

LightGBM is a gradient boosting framework based on tree-based learning algorithms and histogram-based optimization.

It is designed to provide efficient training and prediction performance.

---

## 7. Random Forest — Extension

Random Forest was introduced as an extension to the reference-model comparison.

Random Forest is an ensemble learning method that combines multiple decision trees to produce a final prediction.

It was evaluated using the same dataset, preprocessing strategy and train-test split as the other models.

---

# ⚖️ Balanced Random Forest Experiment

Because the dataset contains only 495 bankrupt companies compared with 10,008 non-bankrupt companies, class imbalance is a major issue.

An additional **Balanced Random Forest** experiment was therefore conducted using class weighting.

The purpose was to determine whether giving greater importance to the minority bankruptcy class could improve bankruptcy detection.

The experiment specifically examined:

- Accuracy
- Bankruptcy precision
- Bankruptcy recall
- Bankruptcy F1-score

The result showed that class weighting increased bankruptcy precision but did not improve bankruptcy recall.

---

# 📏 Evaluation Metrics

The models were evaluated using multiple metrics rather than relying only on accuracy.

## Accuracy

Measures the overall proportion of correctly classified companies.

```text
Accuracy = Correct Predictions / Total Predictions
```

Although useful, accuracy can be misleading for highly imbalanced datasets.

---

## Log Loss

Log Loss evaluates the quality of the predicted probabilities.

Lower values indicate better probabilistic predictions.

---

## Precision

Precision measures how many companies predicted as bankrupt were actually bankrupt.

```text
Precision = True Positives / (True Positives + False Positives)
```

High precision means that when the model predicts bankruptcy, the prediction is more likely to be correct.

---

## Recall

Recall measures how many of the actual bankrupt companies were successfully detected.

```text
Recall = True Positives / (True Positives + False Negatives)
```

For this project, recall is particularly important because failing to identify an actually bankrupt company can be more important than overall classification accuracy.

---

## F1-Score

F1-score provides a balance between precision and recall.

```text
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

---

## Confusion Matrix

The confusion matrix provides a class-by-class view of correct and incorrect predictions.

It helps identify:

- True negatives
- False positives
- False negatives
- True positives

---

# 🔁 Cross-Validation

A **5-fold Stratified Cross-Validation** procedure was performed to evaluate model consistency.

Stratification ensures that each fold maintains a representative distribution of the two target classes.

Mean imputation was included inside the cross-validation pipeline to prevent information from the validation folds from leaking into the training process.

The following cross-validation metrics were recorded:

- Mean CV Accuracy
- Mean CV Log Loss

---

# 📈 Results

The following table summarizes the model comparison obtained in the project.

| Model | Test Accuracy | Test Log Loss | CV Accuracy | CV Log Loss |
|---|---:|---:|---:|---:|
| Logistic Regression | 95.10% | 0.222 | 95.12% | 0.219 |
| SVM | 95.29% | 0.190 | 95.29% | 0.190 |
| Neural Network | 95.29% | 0.189 | 95.29% | 0.188 |
| Bernoulli Naive Bayes | 76.39% | 2.326 | 76.44% | 2.442 |
| XGBoost | 95.29% | 0.178 | 95.29% | 0.175 |
| LightGBM | 95.29% | 0.178 | 95.29% | 0.174 |
| **Random Forest** | **95.86%** | **0.190** | **96.03%** | **0.171** |

Random Forest achieved the highest observed test accuracy and cross-validation accuracy among the models evaluated in this project.

---

# ⚠️ Class Imbalance Results

The dataset's class imbalance significantly affected bankruptcy detection.

The Balanced Random Forest experiment produced:

| Metric | Random Forest | Balanced Random Forest |
|---|---:|---:|
| Accuracy | 95.86% | 95.95% |
| Bankruptcy Precision | 75% | **89%** |
| Bankruptcy Recall | **18%** | 16% |
| Bankruptcy F1 | 29% | 27% |

The Balanced Random Forest increased bankruptcy precision from **75% to 89%**.

However, bankruptcy recall decreased from **18% to 16%**.

Therefore, class weighting alone did not improve the detection of the minority bankruptcy class in this experiment.

---

# 🔎 Key Findings

The experiments produced several important observations.

### 1. Random Forest achieved the highest overall performance

Random Forest achieved:

```text
Test Accuracy: 95.86%
Cross-Validation Accuracy: 96.03%
Cross-Validation Log Loss: 0.171
```

among the models evaluated in the project.

### 2. Accuracy alone is not sufficient

The dataset is highly imbalanced, with:

```text
10,008 non-bankrupt companies
495 bankrupt companies
```

Therefore, a model can obtain high overall accuracy while still failing to identify a large proportion of bankrupt companies.

### 3. Bankruptcy recall remains low

Despite high overall accuracy, the original Random Forest detected only 18% of the actual bankrupt companies.

This demonstrates why minority-class recall must be considered alongside accuracy.

### 4. Balanced Random Forest increased precision but reduced recall

The Balanced Random Forest achieved:

```text
Bankruptcy Precision: 89%
Bankruptcy Recall:    16%
Bankruptcy F1-score:  27%
```

This means the model became more precise when predicting bankruptcy, but it detected an even smaller proportion of the actual bankrupt companies.

### 5. Bernoulli Naive Bayes performed substantially worse

Bernoulli Naive Bayes achieved:

```text
Test Accuracy: 76.39%
Test Log Loss: 2.326
```

which was substantially weaker than the other evaluated models.

---

# 🧠 Interpretation

The results demonstrate an important issue in financial classification:

> High overall accuracy does not necessarily mean that a model is effective at identifying bankrupt companies.

Because bankruptcy is the minority class, evaluation should not rely solely on accuracy.

Precision, recall and F1-score for the bankruptcy class provide additional information about how effectively the model detects financially distressed companies.

The Balanced Random Forest experiment further demonstrated that simply applying class weighting does not automatically solve the minority-class detection problem.

---

# 🛠️ Technologies Used

The project was implemented in Python using:

- Python
- Pandas
- NumPy
- SciPy
- Scikit-learn
- XGBoost
- LightGBM
- Matplotlib
- Jupyter Notebook

---

# 📁 Project Structure

```text
Corporate-Bankruptcy-Prediction-ML/
│
├── 3year.arff
│
├── Notebook.ipynb
│
├── final_model_results.csv
│
├── balanced_random_forest_results.csv
│
├── README.md
│
└── Corporate-Bankruptcy-Prediction-Using-Machine-Learning.pdf
```

The exact filenames may vary depending on the version of the project uploaded to the repository.

---

# 📓 Notebook

The Jupyter Notebook contains the implementation of the complete machine learning workflow, including:

1. Dataset loading
2. Data exploration
3. Missing-value analysis
4. Mean imputation
5. Feature and target separation
6. Train-test splitting
7. Model training
8. Model prediction
9. Metric calculation
10. Confusion matrix generation
11. Cross-validation
12. Model comparison
13. Random Forest extension
14. Balanced Random Forest experiment
15. Final result analysis

---

# 🔬 Research Paper

The project is based on a research study on corporate bankruptcy prediction using financial indicators of Polish companies.

The reference study investigated:

- Logistic Regression
- Support Vector Machine
- Neural Network
- Naive Bayes
- Extreme Gradient Boosting
- Light Gradient Boosting Machine

The study evaluated models using accuracy, log loss, training time and confusion matrices.

The research paper reported that SVM performed strongly in its original experiments, while Logistic Regression and Neural Network also showed strong performance. Naive Bayes performed comparatively poorly, and the gradient boosting approaches required further investigation.

This project reproduces the reference-model comparison while adding Random Forest as an extension.

---

# 🔄 Reproduction and Extension

The project consists of two major parts.

## Part 1 — Reproduction

The following six models correspond to the models investigated in the reference study:

```text
1. Logistic Regression
2. Support Vector Machine
3. Neural Network
4. Bernoulli Naive Bayes
5. XGBoost
6. LightGBM
```

The models were evaluated using the same dataset and a consistent experimental workflow.

## Part 2 — Extension

Random Forest was added as an additional machine learning model:

```text
Random Forest
```

The extension was followed by an additional experiment:

```text
Balanced Random Forest
```

to investigate whether class weighting could improve minority-class bankruptcy detection.

---

# 📌 Limitations

The project has several limitations.

### Class Imbalance

The dataset is strongly imbalanced toward non-bankrupt companies.

This makes overall accuracy less informative when evaluating bankruptcy detection.

### Minority-Class Detection

The models achieved high overall accuracy but relatively low recall for the bankruptcy class.

### Feature Standardization

Feature standardization was not applied, following the methodology used in the project/reference approach.

### Class Weighting

The Balanced Random Forest experiment showed that class weighting alone was insufficient to improve bankruptcy recall.

---

# 🚀 Future Work

Possible directions for future improvement include:

- Synthetic feature generation
- More advanced class-imbalance techniques
- Oversampling methods such as SMOTE
- Undersampling techniques
- Hyperparameter optimization
- Threshold optimization for bankruptcy detection
- Feature selection
- Feature engineering
- Ensemble methods
- Cost-sensitive learning
- Explainable machine learning
- Additional evaluation using ROC-AUC and PR-AUC
- Comparison with additional modern classification models

The reference study itself suggested exploring synthetic feature generation and newer approaches to improve performance on this type of data.

---

# 👥 Team Members

### Amoghaar R
PES University  
SRN: PES2UG24CS625

### Ramya
PES University  
SRN: PES2UG24CS653

---

# 📚 References

1. Reference research paper — *Corporate Bankruptcy Prediction*.
2. Polish Companies Bankruptcy Dataset — UCI Machine Learning Repository.
3. Scikit-learn documentation.
4. XGBoost documentation.
5. LightGBM documentation.
6. Relevant research literature on corporate bankruptcy prediction and machine learning.

---

# 📜 Conclusion

This project implemented and compared multiple machine learning classification algorithms for predicting corporate bankruptcy using financial indicators from the Polish Companies Bankruptcy Dataset.

Random Forest produced the highest observed overall and cross-validation accuracy in the extended experiment.

However, the results also demonstrate that high accuracy does not necessarily translate into effective detection of bankrupt companies because of the severe class imbalance.

The Balanced Random Forest experiment increased bankruptcy precision but reduced bankruptcy recall, showing that class weighting alone was not sufficient to improve minority-class detection.

Therefore, corporate bankruptcy prediction should be evaluated using a combination of:

```text
Accuracy
+
Precision
+
Recall
+
F1-Score
+
Log Loss
+
Confusion Matrix
```

rather than relying on accuracy alone.
```

One important correction compared with some of the earlier PPT wording: **Random Forest is the extension, not one of the six reference models.** Your own project report explicitly describes the six reference models and then Random Forest as the additional model, followed by the Balanced Random Forest experiment. :chatgpt-content-reference{index="0"}

Also, the actual project report confirms the dataset size, 64 features, 80:20 split, mean imputation, 5-fold stratified CV, and the final results above. :chatgpt-content-reference{index="1"} :chatgpt-content-reference{index="2"}

This is the version I'd put in the GitHub repository.
