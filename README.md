# **Body Fat Percentage Prediction Using Regression Techniques**

## **Project Overview**
This project focuses on predicting body fat percentage using various body measurements. The dataset contains multiple features, such as weight, height, adiposity, and wrist size. The objective was to compare different regression models and evaluate their performance in terms of predictive accuracy, handling multicollinearity, and model stability.

The key techniques applied include multiple linear regression, Ridge, LASSO, Principal Component Regression (PCR), and Partial Least Squares (PLS). Extensive validation was conducted using Monte Carlo Cross Validation to assess model performance.

## **Table of Contents**
- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Models Used](#models-used)
- [Model Comparison](#model-comparison)
- [Findings and Conclusions](#findings-and-conclusions)
- [Installation and Usage](#installation-and-usage)
- [Results](#results)
- [References](#references)

---

## **Dataset**
The dataset includes body measurements such as weight, height, adiposity, neck, chest, abdomen, hip, thigh, knee, ankle, biceps, forearm, and wrist. The target variable is body fat percentage (Brozek formula). A split was made between training and testing data to evaluate model generalization.

- **Features:**
  - Weight, Height, Neck, Chest, Abdomen, Hip, Thigh, Knee, Ankle, Biceps, Forearm, Wrist
  - Derived features like adiposity (BMI), density, and more
- **Target:**
  - Brozek body fat percentage

---

## **Models Used**

1. **Linear Regression**:
   A baseline model using all available predictors. This model provided the foundation for evaluating more advanced techniques. 

2. **Ridge Regression**:
   Applied regularization to handle multicollinearity by penalizing large coefficients. This helped reduce overfitting and made the model more stable.

3. **LASSO Regression**:
   A regularized method that performs both variable selection and regularization. This was used to identify the most important features.

4. **Principal Component Regression (PCR)**:
   Applied dimensionality reduction by transforming the original predictors into principal components. This helped address multicollinearity by using a smaller subset of components.

5. **Partial Least Squares (PLS)**:
   Similar to PCR but designed to maximize the covariance between the predictors and the target variable. PLS was used to further reduce model complexity.

---

## **Model Comparison**
The table below shows the performance of different models after 100 iterations of Monte Carlo Cross Validation:

| **Model**              | **MSE**  | **AVG MSE**  | **Variance of MSE** | **Predictors Selected**     |
|------------------------|----------|--------------|---------------------|----------------------------|
| Linear Regression (Full) | 0.04650  | 0.09794975   | 0.031525815          | All 17 Predictors           |
| Linear Regression (k=5)  | 0.05060  | 0.03490135   | 0.0004733885         | siri, knee, wrist, thigh, age |
| Stepwise Regression      | 0.04671  | 0.10173742   | 0.038722597          | siri, weight, height, free, knee, wrist |
| Ridge Regression         | 0.04639  | 0.10079577   | 0.035145436          | All 17 Predictors           |
| LASSO Regression         | 0.04923  | 0.08642128   | 0.027429771          | All 17 Predictors           |
| PCR                      | 0.04650  | 0.09794975   | 0.031525815          | All Components (17)         |
| PLS                      | 0.04650  | 0.09794975   | 0.031525815          | All Components (17)         |

### Key Insights:
- **Full Linear Regression & PCR & PLSR**:  Due to all 17 predictors being selected in 
the three models, the PCR and PLSR model is equivalent to the full regression 
model and the three models yielded the same results. Since the full model exhibits 
multicollinearity, PCR and PLSR here will exhibit the same issues.

- **Linear Regression (k = 5 Subset Model)**: The subset model with only 5 predictors 
(siri, knee, wrist, thigh, and age) showed the lowest AVG MSE and least variance 
across cross-validation runs, indicating a more stable model. The model does not 
exhibit multicollinearity issues.

- **Stepwise Linear Regression:**: The stepwise model selected variables using AIC, has 
the highest AVG MSE (0.10173742), and showed the largest variance (0.038722597) 
across cross-validations, highlighting some instability in performance. Thus, not the 
best model. The model also has multicollinearity issues checked using VIF method. 
The predictors siri (VIF = 23.71), weight (VIF = 47.88), and free (VIF = 34.90) have very 
high VIF values, indicating substantial multicollinearity.

- **Lasso Regression:**: The stepwise model selected variables using AIC, has 
the highest AVG MSE (0.10173742), and showed the largest variance (0.038722597) 
across cross-validations, highlighting some instability in performance. Thus, not the 
best model. The model also has multicollinearity issues checked using VIF method. 
The predictors siri (VIF = 23.71), weight (VIF = 47.88), and free (VIF = 34.90) have very 
high VIF values, indicating substantial multicollinearity.

---

