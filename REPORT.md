# Customer Churn Analysis and Prediction Report

## Introduction
Customer churn is a significant issue for businesses, particularly in the telecommunications sector. This report details the analysis and prediction of customer churn using a dataset from a telecommunications company. The project includes data preprocessing, exploratory data analysis (EDA), feature engineering, model building, and evaluation. The objective is to develop a predictive model to identify customers likely to churn, allowing the company to take proactive measures to retain them. This report provides a comprehensive understanding of the methods used, insights gained, and recommendations based on the analysis.

## Data Loading and Overview
The dataset used for this analysis is sourced from Kaggle's Telco Customer Churn dataset. It includes customer demographics, account details, and services subscribed to by customers. The dataset contains 7,043 rows and 21 columns. Key columns include:

- **customerID**: Unique identifier for each customer.
- **gender**: Gender of the customer (Male/Female).
- **SeniorCitizen**: Whether the customer is a senior citizen (1) or not (0).
- **Partner**: Whether the customer has a partner (Yes/No).
- **Dependents**: Whether the customer has dependents (Yes/No).
- **tenure**: Number of months the customer has stayed with the company.
- **PhoneService**: Whether the customer has a phone service (Yes/No).
- **MultipleLines**: Whether the customer has multiple lines (No, Yes, No phone service).
- **InternetService**: Customer’s internet service provider (DSL, Fiber optic, No).
- **OnlineSecurity**: Whether the customer has online security (Yes, No, No internet service).
- **OnlineBackup**: Whether the customer has online backup (Yes, No, No internet service).
- **DeviceProtection**: Whether the customer has device protection (Yes, No, No internet service).
- **TechSupport**: Whether the customer has tech support (Yes, No, No internet service).
- **StreamingTV**: Whether the customer streams TV (Yes, No, No internet service).
- **StreamingMovies**: Whether the customer streams movies (Yes, No, No internet service).
- **Contract**: The contract term of the customer (Month-to-month, One year, Two year).
- **PaperlessBilling**: Whether the customer has paperless billing (Yes/No).
- **PaymentMethod**: The customer’s payment method (Electronic check, Mailed check, Bank transfer (automatic), Credit card (automatic)).
- **MonthlyCharges**: The amount charged to the customer monthly.
- **TotalCharges**: The total amount charged to the customer.
- **Churn**: Whether the customer churned (Yes/No).

## Understanding the Dataset
The dataset provides a comprehensive overview of the customers and their behavior. It includes demographic information such as gender, whether the customer is a senior citizen, whether they have a partner, and whether they have dependents. It also includes information about the services they subscribe to, such as phone service, multiple lines, internet service, online security, online backup, device protection, tech support, streaming TV, and streaming movies.

Additionally, the dataset includes account information such as the tenure (number of months the customer has stayed with the company), contract type (month-to-month, one year, two year), paperless billing, payment method, monthly charges, and total charges. The target variable in the dataset is Churn, which indicates whether the customer has churned or not.

## Data Cleaning and Preprocessing
### Handling Missing Values
One of the first steps in the data cleaning process was to handle missing values. The TotalCharges column had some missing values. These were converted to numeric values, and rows with missing values were dropped. The customerID column was removed as it is not relevant for the analysis. This step ensures that the data used for modeling is complete and accurate.

### Encoding Categorical Data
The dataset contains several categorical variables that need to be converted into a numerical format suitable for machine learning models. One-hot encoding was used to achieve this. This process involved creating binary columns for each category in the categorical variables. For example, the gender column was converted into two columns: gender_Male and gender_Female, with values of 0 or 1 indicating the presence of that category.

### Feature Scaling
Feature scaling is an important step in preprocessing, especially for models that are sensitive to the scale of the data, such as logistic regression and gradient boosting. The StandardScaler from scikit-learn was used to standardize the features by removing the mean and scaling to unit variance. This ensures that all features contribute equally to the model.

## Exploratory Data Analysis (EDA)
### Distribution of Numerical Data
Analyzing the distribution of numerical data helps in understanding the data's spread and central tendency.

- **Tenure**: The tenure variable, which represents the number of months a customer has stayed with the company, has a right-skewed distribution. This indicates that many customers are relatively new and have shorter tenures.

- **Monthly Charges**: The monthly charges variable has a fairly normal distribution with a slight skew towards higher values. This suggests that while most customers are charged around the average monthly fee, a small number of customers are charged significantly more.

- **Total Charges**: The total charges variable has a distribution similar to tenure, as it depends on the number of months a customer has been with the company and their monthly charges.

### Churn Distribution
The target variable Churn is imbalanced, with a higher proportion of customers not churning compared to those who do. Specifically, about 27% of customers have churned, while 73% have not. Understanding this distribution is crucial for model building and evaluation, as imbalanced data can bias the model towards the majority class.

### Feature Distribution by Churn
Visualizing the distribution of features with respect to churn helps in identifying patterns and insights.

- **Gender**: There is no significant difference in churn rates between male and female customers, indicating that gender does not play a major role in customer churn.

- **Senior Citizens**: Senior citizens have a higher churn rate compared to non-senior citizens. This suggests that senior citizens might have specific needs or preferences that are not being met.

- **Dependents**: Customers with dependents have a lower churn rate compared to those without dependents. This might be because customers with dependents have more stable needs and are less likely to switch providers.

- **Contract Type**: Customers with month-to-month contracts have the highest churn rates, while those with one or two-year contracts have much lower churn rates. This indicates that long-term contracts are effective in retaining customers.

- **Payment Method**: Customers using electronic checks have a higher churn rate compared to those using other payment methods. This could be due to the perceived inconvenience or higher risk associated with electronic checks.

- **Additional Services**: Customers subscribing to additional services such as online security, online backup, and tech support are less likely to churn. This suggests that these services add value and increase customer loyalty.

### Correlation Analysis
Correlation analysis was conducted to understand the relationships between different variables. The correlation matrix showed that tenure and TotalCharges are highly correlated, which is expected since TotalCharges is a function of tenure and MonthlyCharges. Other notable correlations include the relationships between Contract type and churn, and between PaymentMethod and churn.

## Feature Engineering
Feature engineering was conducted to create additional relevant features and enhance the model's predictive power. New features included interaction terms and derived features from the existing variables. For example, the interaction between tenure and Contract type was considered, as longer tenure combined with long-term contracts could indicate lower churn probability.

## Handling Imbalanced Data
Imbalanced datasets can bias the model towards the majority class, leading to poor performance in predicting the minority class. To address this, techniques like SMOTEENN (a combination of SMOTE and ENN) were used to resample the data. SMOTE (Synthetic Minority Over-sampling Technique) generates synthetic samples for the minority class by interpolating between existing minority samples. ENN (Edited Nearest Neighbors) cleans the dataset by removing noisy samples that are misclassified by their nearest neighbors.

## Model Training and Evaluation
Several models were trained and evaluated to determine the best performing model for predicting customer churn.

### Logistic Regression
Logistic Regression was used as a baseline model for binary classification. It provided decent performance but struggled with the imbalanced nature of the data. The model was trained on the preprocessed data, and the following performance metrics were observed:

| Model               | Accuracy | Precision (Class 0) | Precision (Class 1) | Recall (Class 0) | Recall (Class 1) | F1-Score (Class 0) | F1-Score (Class 1) |
|---------------------|----------|---------------------|---------------------|------------------|------------------|--------------------|--------------------|
| Logistic Regression | 0.91     | 0.91                | 0.92                | 0.90             | 0.92             | 0.90               | 0.92               |

### Decision Tree
A Decision Tree model was trained to capture non-linear relationships in the data. It provided better interpretability but was prone to overfitting and did not generalize well to unseen data. The following performance metrics were observed:

| Model            | Accuracy | Precision (Class 0) | Precision (Class 1) | Recall (Class 0) | Recall (Class 1) | F1-Score (Class 0) | F1-Score (Class 1) |
|------------------|----------|---------------------|---------------------|------------------|------------------|--------------------|--------------------|
| Decision Tree    | 0.93     | 0.94                | 0.93                | 0.91             | 0.94             | 0.92               | 0.94               |

### Random Forest
A Random Forest model was trained to improve performance and reduce overfitting. Random Forests combine multiple decision trees to provide more robust predictions. The model showed significant improvement in performance metrics:

| Model           | Accuracy | Precision (Class 0) | Precision (Class 1) | Recall (Class 0) | Recall (Class 1) | F1-Score (Class 0) | F1-Score (Class 1) |
|-----------------|----------|---------------------|---------------------|------------------|------------------|--------------------|--------------------|
| Random Forest   | 0.95     | 0.96                | 0.94                | 0.93             | 0.96             | 0.94               | 0.95               |


### XGBoost
XGBoost, an optimized implementation of gradient boosting, was used for its efficiency and performance. It provided the best results among the models evaluated:

| Model | Accuracy | Precision (Class 0) | Precision (Class 1) | Recall (Class 0) | Recall (Class 1) | F1-Score (Class 0) | F1-Score (Class 1) |
|--------------------|----------|---------------------|---------------------|------------------|------------------|--------------------|--------------------|
| XGBoost | 0.96     | 0.96                | 0.95                | 0.94             | 0.97             | 0.95               | 0.96               |

## Insights from XGBoost Model

The high accuracy and balanced performance metrics of the XGBoost model indicate its robustness in handling the dataset's complexity and imbalanced nature. Its ability to handle non-linear relationships and interactions between features contributes to its superior performance.

- Accuracy: 96%
- Precision (Class 0): 96%
- Precision (Class 1): 96%
- Recall (Class 0): 95%
- Recall (Class 1): 97%
- F1-Score (Class 0): 95%
- F1-Score (Class 1): 96%

The XGBoost model's ability to handle a large number of features and its robustness against overfitting make it an ideal choice for predicting customer churn. Its high precision and recall for both classes indicate that it is effective in correctly identifying both churned and non-churned customers, minimizing false positives and false negatives.

## Challenges Faced

Several challenges were encountered during the analysis and modeling process.

### Imbalanced Data

The imbalanced nature of the dataset posed a challenge in model training. Imbalanced data can lead to biased models that favor the majority class, resulting in poor performance in predicting the minority class. Techniques such as SMOTEENN were employed to address this issue. SMOTEENN combines synthetic minority over-sampling with edited nearest neighbors to create a more balanced dataset that is also cleaned of noisy samples.

### Feature Engineering

Creating meaningful features from the existing data required a deep understanding of the domain and careful consideration of feature interactions. For example, the interaction between tenure and Contract type was considered, as longer tenure combined with long-term contracts could indicate lower churn probability. Feature engineering is a critical step in improving model performance, but it requires domain expertise and careful analysis.

### Hyperparameter Tuning

Finding the optimal hyperparameters for the models was computationally intensive and required significant time and resources. Hyperparameter tuning involves adjusting the parameters of the model to find the best combination that results in the highest performance. Techniques such as grid search and random search were used to explore the hyperparameter space, but this process can be time-consuming and resource-intensive.

### Data Cleaning

Handling missing values and encoding categorical data accurately was crucial for the success of the models. Missing values in the TotalCharges column were converted to numeric values, and rows with missing values were dropped. Categorical variables were encoded using one-hot encoding to convert them into a numerical format suitable for machine learning models. Accurate data cleaning and preprocessing are essential to ensure the quality and reliability of the models.


## Conclusion and Recommendations
The analysis and predictive modeling identified several key factors influencing customer churn. Long-term contracts, additional services (like online security and tech support), and specific payment methods were found to be significant in reducing churn rates.

Based on the analysis, the following recommendations are made to reduce customer churn:

1. **Promote Long-Term Contracts**: Encouraging customers to sign up for one or two-year contracts can significantly reduce churn rates.

2. **Enhance Service Offerings**: Providing value-added services such as online security, online backup, and tech support can improve customer retention.

3. **Optimize Payment Methods**: Offering incentives for customers to use more stable payment methods (like bank transfers or credit cards) can help reduce churn.

4. **Targeted Interventions for Senior Citizens**: Developing specific programs or offers for senior citizens can address their higher churn rates.

5. **Focus on High-Risk Customers**: Utilizing the predictive model to identify high-risk customers and offering them targeted retention strategies can be effective in reducing churn.

By implementing these strategies, the company can proactively reduce customer churn and improve overall customer satisfaction and loyalty. The predictive model developed in this project provides a valuable tool for identifying at-risk customers and tailoring interventions accordingly.
