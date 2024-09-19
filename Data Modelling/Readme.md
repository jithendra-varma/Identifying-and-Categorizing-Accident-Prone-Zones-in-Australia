# Machine Learning Workflow for Accident-Prone Zone Classification

## Introduction

This workflow focuses on classifying accident-prone zones based on various features derived from road crash data. The aim is to develop and evaluate machine learning models that can accurately predict the severity of accident-prone zones. The process includes data loading, preprocessing, model training, evaluation, and analysis of feature importance.

## Data Loading and Preparation

### Data Overview

The data is loaded from a CSV file named `Clustered_Data.csv`. The dataset contains 64,087 entries with 16 features, including accident counts, average severity, light conditions, weather conditions, and other relevant metrics. These features are crucial for understanding the factors contributing to road accidents.

### Target Variable and Features

The target variable in this study is `accident_prone_zone_rating`, which categorizes accident-prone zones into three levels: `Low`, `Mid`, and `High`. The feature set includes numerical columns that describe various characteristics of accidents, such as the number of accidents, average severity, and environmental conditions at the time of the accidents.

### Data Cleaning and Preprocessing

Before training the models, several preprocessing steps were taken:

1. **Dropping Irrelevant Columns:** Columns such as location details, geographic identifiers, and other non-predictive variables were removed to streamline the dataset.

2. **Categorical and Numerical Columns:** The dataset mainly consists of numerical features. Any remaining categorical features were identified for encoding, while numerical features were standardized to ensure uniformity across the data.

3. **Handling Missing Data:** Simple imputation techniques were used to fill in missing values, ensuring that the dataset was complete and ready for modeling.

4. **Feature Scaling:** Numerical features were standardized to have a mean of 0 and a standard deviation of 1, which is essential for the performance of machine learning algorithms.

5. **Handling Class Imbalance:** The dataset had an imbalance in the target variable categories. To address this, the Synthetic Minority Over-sampling Technique (SMOTE) was employed to balance the classes, particularly ensuring that the minority class (`High` accident-prone zones) was adequately represented.

## Model Development

### Model Selection

Three machine learning models were selected for this task:

- **Random Forest Classifier:** A robust ensemble learning method that aggregates predictions from multiple decision trees to improve accuracy and control over-fitting.
- **Support Vector Machine (SVM):** A powerful algorithm for classification tasks, especially effective in high-dimensional spaces.
- **Gradient Boosting Classifier:** An advanced ensemble technique that builds models sequentially, with each new model correcting errors made by previous ones.

These models were chosen due to their effectiveness in handling classification tasks and their ability to work well with both small and large datasets.

### Model Training

The models were trained on the preprocessed data. The dataset was split into training and testing sets, with the training set used to fit the models and the testing set reserved for evaluation. Cross-validation was also employed to ensure that the models were robust and to prevent overfitting.

### Model Evaluation

The models were evaluated using several metrics:

- **Accuracy:** The proportion of correct predictions made by the model.
- **Balanced Accuracy:** A more balanced version of accuracy that takes into account the performance across all classes, especially in imbalanced datasets.
- **Recall:** The ability of the model to correctly identify true positives.
- **Precision:** The accuracy of the positive predictions made by the model.
- **F1 Score:** The harmonic mean of precision and recall, providing a single metric to evaluate model performance.
- **Confusion Matrix:** A table used to describe the performance of the classification model, showing the true positive, true negative, false positive, and false negative predictions.

### Best Model Selection

Among the models, Gradient Boosting Classifier emerged as the best-performing model based on the Balanced Accuracy metric. This model demonstrated the highest ability to correctly classify accident-prone zones across all categories (`Low`, `Mid`, `High`).

## Model Testing and Results

The selected model (Gradient Boosting) was tested on the unseen test set. The model's performance on the test set closely matched its performance during cross-validation, indicating that it generalizes well to new data.

- **Test Set Metrics:** The model achieved high scores in accuracy, balanced accuracy, recall, precision, and F1 score, affirming its reliability in predicting accident-prone zones.

## Feature Importance Analysis

For models like Random Forest and Gradient Boosting, feature importance was analyzed to understand which factors contributed most to the classification of accident-prone zones. The analysis revealed that:

- **Accident Count:** The most critical feature, indicating that the number of accidents is a strong predictor of whether a zone is `Low`, `Mid`, or `High`.
- **Speed Limits:** Speed-related features (e.g., whether the speed limit is above or below 60 km/h) also played a significant role in determining the severity of an accident-prone zone.
- **Environmental Conditions:** Features such as light conditions and weather conditions were less influential but still contributed to the model's predictions.

## Conclusion

The workflow successfully developed a machine learning model capable of classifying accident-prone zones with high accuracy. The Gradient Boosting Classifier, in particular, provided the best results and demonstrated strong generalization to new data. This model, along with the insights gained from feature importance analysis, can be used to inform policy decisions and improve road safety by identifying and addressing high-risk areas.
