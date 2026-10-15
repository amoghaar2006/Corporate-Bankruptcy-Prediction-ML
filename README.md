# Corporate Bankruptcy Prediction Using Machine Learning

A machine learning project that predicts corporate bankruptcy using financial indicators from the Polish Companies Bankruptcy Dataset.

## 📌 Project Overview

Corporate bankruptcy prediction is a binary classification problem that uses financial data to identify companies that may be at risk of bankruptcy.

This project implements and compares six machine learning models discussed in a reference research study and extends the comparison using Random Forest. An additional Balanced Random Forest experiment investigates the impact of class weighting on minority-class bankruptcy detection.

The project emphasizes not only overall predictive performance but also the challenges of detecting bankrupt companies in a highly imbalanced dataset.

## 🎯 Objectives

- Predict corporate bankruptcy using financial indicators.
- Implement and compare six reference models.
- Extend the comparison using Random Forest.
- Evaluate performance using accuracy, log loss, precision, recall, and F1-score.
- Perform 5-fold stratified cross-validation.
- Analyze the impact of class imbalance on bankruptcy prediction.
- Investigate whether Balanced Random Forest improves minority-class detection.

## 📊 Dataset

**Dataset:** Polish Companies Bankruptcy Dataset  
**Source:** UCI Machine Learning Repository  
**Selected file:** `3year.arff`

| Property | Value |
|---|---:|
| Total instances | 10,503 |
| Financial features | 64 |
| Non-bankrupt companies | 10,008 |
| Bankrupt companies | 495 |
| Classification type | Binary |

The dataset is highly imbalanced, with substantially more non-bankrupt companies than bankrupt companies. Consequently, a model can achieve high accuracy while failing to detect many actual bankruptcies.

## 🧹 Data Preprocessing

The following preprocessing steps were performed:

1. Loaded the ARFF dataset into a Pandas DataFrame.
2. Separated the financial features and target variable.
3. Handled missing values using mean imputation.
4. Split the data into training and testing sets using an 80:20 stratified split.
5. Used the same split for all models to ensure a consistent comparison.
6. Included imputation within the cross-validation pipeline to prevent data leakage.

| Dataset split | Instances |
|---|---:|
| Training set | 8,402 |
| Testing set | 2,101 |

Feature standardization was not applied in the reported experimental workflow.

## 🔬 Methodology

```text
Dataset Loading
       ↓
Data Preprocessing
       ↓
Missing Value Imputation
       ↓
Stratified Train-Test Split
       ↓
Model Training and Prediction
       ↓
Performance Evaluation
       ↓
5-Fold Stratified Cross-Validation
       ↓
Model Comparison
       ↓
Class Imbalance Analysis
```

## 🤖 Machine Learning Models

### Reference Models

The project implements the six models investigated in the reference study.

1. **Logistic Regression:** Estimates the probability of bankruptcy using a logistic function.
2. **Support Vector Machine (SVM):** Identifies a decision boundary that separates the classes.
3. **Multilayer Perceptron (MLP):** A neural network capable of learning nonlinear patterns.
4. **Bernoulli Naive Bayes:** A probabilistic classifier based on Bayes' theorem and conditional independence assumptions.
5. **XGBoost:** A gradient boosting algorithm that combines multiple decision trees.
6. **LightGBM:** A gradient boosting framework designed for efficient tree-based learning.

### Additional Model: Random Forest

Random Forest was added as an extension to the reference-model comparison. It combines predictions from multiple decision trees to produce a final classification.

### Balanced Random Forest Experiment

An additional experiment investigated the effect of class weighting on bankruptcy detection. The aim was to improve the model's ability to identify companies belonging to the minority bankruptcy class.

## 📏 Evaluation Metrics

The models were evaluated using the following metrics:

- **Accuracy:** Proportion of correctly classified companies.
- **Log Loss:** Measures the quality of predicted probabilities; lower values are better.
- **Precision:** Proportion of predicted bankrupt companies that were actually bankrupt.
- **Recall:** Proportion of actual bankrupt companies correctly identified.
- **F1-score:** Harmonic mean of precision and recall.
- **Confusion Matrix:** Summarizes true positives, true negatives, false positives, and false negatives.

Five-fold stratified cross-validation was also used to examine model performance across multiple data splits.

## 📈 Model Comparison Results

The following results were obtained in the reported experiments.

| Model | Test Accuracy | Test Log Loss | CV Accuracy | CV Log Loss |
|---|---:|---:|---:|---:|
| Logistic Regression | 95.10% | 0.222 | 95.12% | 0.219 |
| SVM | 95.29% | 0.190 | 95.29% | 0.190 |
| Neural Network (MLP) | 95.29% | 0.189 | 95.29% | 0.188 |
| Bernoulli Naive Bayes | 76.39% | 2.326 | 76.44% | 2.442 |
| XGBoost | 95.29% | 0.178 | 95.29% | 0.175 |
| LightGBM | 95.29% | 0.178 | 95.29% | 0.174 |
| **Random Forest** | **95.86%** | **0.190** | **96.03%** | **0.171** |

Random Forest achieved the highest test accuracy and cross-validation accuracy among the evaluated models.

## ⚖️ Class Imbalance Analysis

The additional Balanced Random Forest experiment produced the following results.

| Metric | Random Forest | Balanced Random Forest |
|---|---:|---:|
| Accuracy | 95.86% | 95.95% |
| Bankruptcy Precision | 75% | 89% |
| Bankruptcy Recall | 18% | 16% |
| Bankruptcy F1-score | 29% | 27% |

Balanced Random Forest increased bankruptcy precision but reduced recall. Therefore, the experiment did not demonstrate an improvement in identifying a larger proportion of actual bankrupt companies.

These findings highlight the limitations of relying on accuracy alone when evaluating models on imbalanced datasets.

## 🔎 Key Findings

1. **Random Forest achieved the highest overall accuracy:** It recorded 95.86% test accuracy and 96.03% cross-validation accuracy.
2. **High accuracy did not guarantee effective bankruptcy detection:** The original Random Forest recall for the bankruptcy class was only 18%.
3. **Class weighting had mixed results:** Balanced Random Forest improved precision to 89%, but recall decreased to 16%.
4. **Bernoulli Naive Bayes performed comparatively poorly:** Its test accuracy was 76.39%.
5. **Multiple evaluation metrics are essential:** Precision, recall, F1-score, and confusion matrices provide information that accuracy alone cannot capture.

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- SciPy
- Scikit-learn
- XGBoost
- LightGBM
- Matplotlib
- Jupyter Notebook

## 📁 Project Structure

```text
Corporate-Bankruptcy-Prediction-ML/
│
├── 3year.arff
├── Notebook.ipynb
├── final_model_results.csv
├── balanced_random_forest_results.csv
├── README.md
└── Corporate-Bankruptcy-Prediction-Using-Machine-Learning.pdf
```

*Note: Update the filenames above to match the files actually present in your GitHub repository.*

## 🔄 Research Reproduction and Extension

The project has two main components.

**Part 1: Reference-model comparison**

- Logistic Regression
- Support Vector Machine
- Neural Network
- Bernoulli Naive Bayes
- XGBoost
- LightGBM

**Part 2: Additional experiments**

- Random Forest
- Balanced Random Forest

The additional experiments extend the comparison and examine whether class weighting improves the detection of bankrupt companies.

## ⚠️ Limitations

- The dataset contains substantially fewer bankrupt companies than non-bankrupt companies.
- High overall accuracy can conceal poor minority-class recall.
- Class weighting alone did not improve bankruptcy recall in the reported Balanced Random Forest experiment.
- Feature standardization was not applied in the reported workflow.
- The results are based on the selected dataset and experimental setup and should not be interpreted as proof of real-world predictive performance.

## 🚀 Future Work

Potential improvements include:

- Hyperparameter tuning.
- Feature selection and feature engineering.
- Oversampling techniques such as SMOTE.
- Undersampling and other class-imbalance methods.
- Decision-threshold optimization.
- Cost-sensitive learning.
- Evaluation using ROC-AUC and PR-AUC.
- Explainable machine learning techniques.
- Further experiments with ensemble classifiers.

## 👥 Team Members

**Amoghaar R**  
PES University  
SRN: PES2UG24CS625

**Ramya**  
PES University  
SRN: PES2UG24CS653

## 📚 References

1. Reference research paper on corporate bankruptcy prediction.
2. Polish Companies Bankruptcy Dataset, UCI Machine Learning Repository.
3. Scikit-learn documentation.
4. XGBoost documentation.
5. LightGBM documentation.
6. Research literature on machine learning for corporate bankruptcy prediction.

*Replace the generic research-paper reference with the exact title, authors, publication venue, year, and DOI or URL of the paper used in the project.*

## 📌 Conclusion

This project compared six reference machine learning models and extended the experiments with Random Forest and Balanced Random Forest for corporate bankruptcy prediction.

Random Forest achieved the highest observed overall accuracy among the evaluated models. However, its low bankruptcy recall demonstrated that strong overall performance does not necessarily translate into effective detection of financially distressed companies.

The Balanced Random Forest experiment increased precision but reduced recall, indicating that class weighting alone was insufficient to improve minority-class detection.

The results emphasize the importance of evaluating bankruptcy prediction systems using multiple metrics, particularly recall, precision, F1-score, and confusion matrices, alongside accuracy and log loss.
