# DiabetesAI: Diabetes Risk Prediction and Health Recommendation System

DiabetesAI is a machine learning project designed to predict diabetes risk using health, behavioral, and healthcare-access indicators. The project uses the 2015 Behavioral Risk Factor Surveillance System (BRFSS) diabetes health indicators dataset from Kaggle to classify individuals by diabetes risk and explore which factors are most associated with diabetes outcomes.

Beyond prediction, this project also explores a health suggestion component that compares diabetic patients to patterns observed among non-diabetic individuals, with the goal of identifying healthier target ranges for indicators such as BMI and general health.

## Project Motivation

Diabetes is one of the most common chronic diseases in the United States and can lead to serious long-term complications if left undiagnosed or unmanaged. Early detection is important because lifestyle changes, medical intervention, and consistent monitoring can help reduce the risk of complications.

This project was motivated by the question:

**Can machine learning help identify individuals at higher risk for diabetes using survey-based health indicators?**

DiabetesAI aims to support early risk identification by using machine learning models to analyze patterns in health-related behaviors, chronic conditions, and healthcare-access variables.

## Dataset

This project uses the cleaned 2015 BRFSS diabetes health indicators dataset from Kaggle. The original BRFSS survey is conducted by the CDC and collects information about health-related risk behaviors, chronic health conditions, and use of preventive services.

The cleaned dataset includes:

- **253,680 survey responses**
- **21 feature variables**
- **1 target variable:** `Diabetes_012`
- No missing values
- A mix of binary, categorical, and continuous features

The original target variable included three classes:

- `0`: No diabetes or only during pregnancy
- `1`: Pre-diabetes
- `2`: Diabetes

Because the pre-diabetes class was very small and difficult to classify accurately, pre-diabetes and diabetes were later combined into a single diabetes-risk class.

## Features Used

The dataset includes health and lifestyle indicators such as:

- High blood pressure
- High cholesterol
- BMI
- Smoking history
- Stroke history
- Heart disease or heart attack
- Physical activity
- Fruit and vegetable consumption
- Heavy alcohol consumption
- General health
- Mental health
- Physical health
- Difficulty walking
- Sex
- Age
- Education
- Income
- Healthcare access

## Methods

### 1. Initial Modeling

The first model was trained using the original three-class diabetes target variable. Logistic Regression was used as an initial baseline model.

The model achieved high overall accuracy, but this was largely due to class imbalance. Since most individuals in the dataset were non-diabetic, the model performed well on the majority class but struggled to identify pre-diabetes and diabetes cases.

### 2. Class Imbalance Handling

To improve risk detection, the target variable was simplified into a binary classification task:

- `0`: Non-diabetic
- `1`: Pre-diabetic or diabetic

The training data was then downsampled so the non-diabetic and diabetic-risk groups were balanced. This helped the model learn from both classes more evenly and improved diabetes-risk detection.

### 3. Feature Selection

Different feature selection approaches were used depending on the model:

- **Random Forest:** tree-based embedded feature importance
- **Support Vector Machine:** recursive feature elimination with cross-validation
- **Logistic Regression:** coefficient-based feature importance

Less relevant features, such as smoking, fruit consumption, vegetable consumption, physical activity, healthcare access, and stroke, were removed during feature selection to improve model performance.

### 4. Model Comparison

The project compared several machine learning models:

- Logistic Regression
- Support Vector Machine
- Random Forest Classifier

Although Random Forest and SVM were expected to capture more complex relationships, Logistic Regression performed the best after preprocessing and feature selection.

## Results

After resampling and feature selection, the Logistic Regression model achieved stronger diabetes-risk classification performance.

Key results:

- **Accuracy:** approximately 74%
- **Precision:** approximately 75% for non-diabetic and 73% for diabetic-risk classification
- **Recall:** approximately 72% for non-diabetic and 76% for diabetic-risk classification

The model showed that survey-based health indicators can provide reasonably useful predictions of diabetes risk, although there is still room for improvement with richer clinical data.

## Health Suggestion Component

In addition to diabetes risk prediction, DiabetesAI explored a recommendation-style component.

This component trained models on non-diabetic individuals to estimate healthier ranges for selected indicators, then applied those patterns to diabetic individuals.

Two indicators were explored:

### BMI Prediction

A Random Forest Regressor was trained on non-diabetic individuals to predict healthier BMI values for diabetic patients.

The model suggested BMI values centered around 25, which falls near the healthy BMI range. However, the prediction error was relatively high, suggesting that additional clinical and lifestyle features would be needed for more personalized recommendations.

### General Health Prediction

A Random Forest Classifier was used to predict general health scores. However, the model often predicted a general health score of 3, corresponding to “good” health. This result was too broad to provide highly specific health recommendations.

This showed that general health is difficult to model from limited survey indicators and would benefit from more detailed health data.

## Key Findings

- Logistic Regression performed best after class balancing and feature selection.
- BMI, general health, and mental health were strongly related to diabetes prediction.
- Class imbalance significantly affected initial model performance.
- Survey-based health data can support semi-accurate diabetes risk prediction.
- More detailed clinical variables, such as medical history, hypertension severity, cholesterol levels, and comorbidities, would likely improve future models.

## Limitations

This project has several limitations:

- The dataset is survey-based and may include self-reporting bias.
- Downsampling reduced the amount of non-diabetic training data.
- The original pre-diabetes class was too small to predict accurately.
- Some health variables were recorded in broad or binary categories, limiting model precision.
- The health suggestion component was exploratory and should not be interpreted as medical advice.

## Future Improvements

Future versions of this project could improve performance by:

- Testing SMOTE or class weighting instead of downsampling
- Trying Gradient Boosting, XGBoost, or neural networks
- Incorporating more detailed clinical health indicators
- Improving feature engineering for behavioral and physiological variables
- Building a more interpretable recommendation system
- Creating a dashboard or web app for diabetes risk visualization

## Tools and Technologies

- Python
- pandas
- NumPy
- scikit-learn
- matplotlib
- seaborn
- Jupyter Notebook
- Logistic Regression
- Random Forest
- Support Vector Machine
- Feature selection
- Classification metrics

## Contributors

- Teresa Zhou
- Charis Xiong
