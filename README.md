# **PHASE 3 PROJECT ON Tanzania WATER WELLS**
# Predicting Water Pump Functionality in Tanzania Using Machine Learning
# Porject Overview

The goal of this project is to:

1. Develop and evaluate machine learning models capable of predicting the operational status of Tanzanian water wells.

2. Apply an iterative modeling approach, starting from a simple baseline (Logistic Regression) and progressing to a more advanced ensemble model (Random Forest Classifier).

3. Compare model performance and interpret key predictors influencing pump functionality.

Ultimately, the project demonstrates how data-driven solutions can optimize decision-making in the water infrastructure sector.


![Tanzania Water Wells Project](Tanzania_water_wells.jpg)






# Business and Data Understanding
# Dataset Description

The dataset comes from the DrivenData “Pump It Up: Data Mining the Water Table” competition
It contains information for over 59,000 water points across Tanzania, with more than 40 features describing geographic, operational, and administrative details.

Target Variable: **status_group**

1. functional

2. non-functional

3. functional needs repair

# Key Features

**amount_tsh** – Total static head (water availability)

**gps_height** – Altitude of the well

**installer** – Who installed the pump

**basin, region, lga** – Location and administrative zones

**extraction_type, management, payment** – Operational and management details

**construction_year** – Installation year of the well

# Business Relevance

The project supports the sustainable management of Tanzania’s water resources by helping identify:

Wells that are likely to fail or need maintenance

High-risk regions where interventions should be prioritized

Factors that most influence well reliability

# Stakeholders

The key stakeholders in this project include:

**Government of Tanzania – Ministry of Water**: Uses insights to guide infrastructure investments and maintenance planning.

**Non-Governmental Organizations (NGOs)**: Partners such as World Bank, WaterAid, and UNICEF who support rural water access projects.

**Local Communities**: Residents relying on boreholes and wells for daily water needs.

**Project Engineers and Data Analysts**: Responsible for maintaining well functionality and using data-driven tools for monitoring.

**Policy Makers**: Use project findings to prioritize regions for intervention and optimize resource allocation.

# Data Loading and Cleaning

Imported data using pandas and inspected its structure and null values.

Below is the data visualization before cleaning

![Target Variable Distribution](images/target_variable_distribution.png)

![Target Variable Distribution](images/Top_10_Founder.png)

![Target Variable Distribution](images/Functional_Status_by_Region.png)
![Target Variable Distribution](images/Distribuition_of_Water_Sources.png)


# Key Insights

**Water Sources Distribution:**
The majority of waterpoints are sourced from springs and shallow wells, followed by machine-drilled boreholes and rivers. Less common sources include rainwater harvesting, hand-dug wells, lakes, dams, and others.

**Functional Status by Region:**
Most waterpoints across regions are functional, though a significant portion are non-functional, and a smaller fraction require repair. This imbalance highlights operational and maintenance challenges, and it’s an important consideration for model training since the target variable is unevenly distributed.

**Funder Distribution:**
The Government of Tanzania is the top funder of water projects, followed by entries labeled as “unknown” (which may need further investigation), Danida, Hesawa, Rwssp, World Bank, Kkkt, World Vision, Unicef, and Tasaf.

**The Following steps were taken to clean the data**

1. Handling of missing Values
2. Conversion of data types & handling inconsistencies.
3. Dropping Reedundant/Low-value Features

   After cleaning following steps were performed to finalize data preparation
1.  Scaling numeric features
2. Encoding categorical variables
3. Encoding the target (status_group)
4. Splitting Data for Modeling


# Modeling

# Baseline Logistic Regression 
a Baselinge ligistic regression model was created and bellow were the model performance

Baseline Logistic Regression Results
Training Accuracy: 0.624125
Testing Accuracy: 0.6375

Classification Report:
              precision    recall  f1-score   support

           0       0.63      0.77      0.69      1007
           1       0.00      0.00      0.00       134
           2       0.65      0.58      0.61       859

    accuracy                           0.64      2000
   macro avg       0.43      0.45      0.44      2000
weighted avg       0.60      0.64      0.61      2000




The baseline logistic regression model achieved a training accuracy of **62.1%** and a testing accuracy of **63.75%**, indicating moderate but limited predictive performance.

**Observations:**

The model performs reasonably well on the majority classes (0 and 2), with F1-scores around 0.62–0.63.

However, it completely fails to predict class 1 (F1-score = 0), suggesting class imbalance — this class likely has very few samples compared to others.

The small gap between training and testing accuracy indicates no significant overfitting, but overall performance is low.

**Insights:**

The low recall and precision for the minority class highlight the need for data balancing techniques (e.g., SMOTE, class weights) or more advanced models (e.g., Random Forest, XGBoost).

This baseline provides a useful benchmark for comparing improved models after feature engineering or resampling.


# Improve the Baseline (Hyperparameter Tuning)

An Improved model was created using the hypermeter tuning and bellow are the results.


Tuned Model Results:
Training Accuracy: 0.636
Testing Accuracy: 0.6455

Classification Report:
              precision    recall  f1-score   support

           0       0.63      0.77      0.70      1007
           1       0.43      0.04      0.08       134
           2       0.67      0.59      0.63       859

    accuracy                           0.65      2000
   macro avg       0.58      0.47      0.47      2000
weighted avg       0.63      0.65      0.63      2000


After hyperparameter tuning, the logistic regression model’s accuracy improved from 63.75% to 64.6%, with better overall balance across classes. However, 
the model still struggles to detect pumps that are functional but need repair, indicating a need for class balancing or more complex algorithms.

# Build a More Complex Model (Random Forest Classifier)

A more complex model was built and yielded the results below.

Training Accuracy: 0.998375
Testing Accuracy: 0.776

Classification Report (Test Set):
              precision    recall  f1-score   support

           0       0.77      0.85      0.81      1007
           1       0.49      0.32      0.39       134
           2       0.81      0.76      0.78       859

    accuracy                           0.78      2000
   macro avg       0.69      0.64      0.66      2000
weighted avg       0.77      0.78      0.77      2000

The Random Forest achieved a significant improvement in performance compared to the Logistic Regression models (which were around 61–62% accuracy). 
The testing accuracy increased to about 76%, showing that the model captures non-linear relationships and feature interactions much better.

However, the training accuracy (99.9%) indicates overfitting — the model fits the training data extremely well but doesn’t generalize perfectly to new data.

Class Performance

Functional wells: Strong precision (0.77) and recall (0.86).

Non-functional wells: Good balance (F1 = 0.74).

Functional needs repair: Still weak (F1 = 0.34), meaning class imbalance remains an issue — the model struggles to detect rare cases.


# Hyperparameter-Tuned Random Forest

Training Accuracy: 0.904625
Testing Accuracy: 0.763

Classification Report (Test Set):
              precision    recall  f1-score   support

           0       0.74      0.87      0.80      1007
           1       0.49      0.14      0.22       134
           2       0.82      0.73      0.77       859

    accuracy                           0.76      2000
   macro avg       0.68      0.58      0.60      2000
weighted avg       0.75      0.76      0.75      2000

This optimized model achieved a training accuracy of 0.904 and a testing accuracy of 0.767, showing a good balance between bias and variance. 
The drop in training accuracy compared to the baseline Random Forest (which was nearly perfect) suggests that the model has reduced overfitting and generalizes better to unseen data.

In terms of class performance:

The model performs very well for “functional” wells (F1 = 0.80) and reasonably well for “non functional” wells (F1 = 0.77).

The “functional needs repair” class remains challenging, with low recall (0.14), reflecting continued class imbalance and limited representation of this category in the training data.

Overall, the tuned Random Forest is the best-performing model so far, offering strong generalization and interpretability. 
It captures non-linear interactions among features and provides a solid foundation for further improvements, such as class weighting or SMOTE balancing.

# Modeling Summary and Final Model Justification
The modeling process followed an iterative approach, beginning with a simple Logistic Regression model as the baseline. 
This initial model achieved a testing accuracy of 0.64, providing a clear starting point for comparison. 
While the model performed moderately well for the majority class (“functional”), it struggled to predict the minority class (“needs repair”), as reflected by its very low recall and F1-score for that category. 
Despite its interpretability, the logistic regression model’s linear nature limited its ability to capture complex relationships in the data.

To improve performance, the model was refined through hyperparameter tuning, adjusting parameters such as the regularization penalty and inverse regularization strength (C). 
The tuned logistic regression model showed a slight improvement, reaching 0.65 testing accuracy. This indicates a marginally better fit but still highlights the limitations of linear 
models when dealing with heterogeneous and non-linear real-world data such as the water pump dataset.

To address these shortcomings, a more complex Random Forest Classifier was introduced. 
This model significantly improved performance, achieving up to 0.78 testing accuracy and better balance across classes. 
The Random Forest was able to capture non-linear patterns and feature interactions that logistic regression could not, leading to stronger generalization and robustness. 
Although it is less interpretable than logistic regression, its higher precision and recall across multiple categories make it a more reliable choice for predicting water pump functionality. 
Therefore, the final model selected is the Tuned Random Forest Classifier, as it offers the best trade-off between predictive accuracy, stability, and practical usefulness for decision-making in water infrastructure management.

# Recommendations and Next Steps
Based on the results of the tuned Random Forest model, it is recommended that this predictive system be integrated into the decision-making process for water pump monitoring and maintenance in Tanzania. 
The model’s high accuracy and reliability in distinguishing between functional, non-functional, and repair-needed pumps can help prioritize maintenance efforts and allocate resources efficiently.
By identifying at-risk pumps before complete failure, local authorities and NGOs can reduce downtime, improve water accessibility, and enhance overall service reliability in rural communities.

For future improvements, several steps are recommended. First, further data enrichment should be explored — for instance, integrating external data such as rainfall patterns, 
population growth, or regional infrastructure investments could improve model accuracy and contextual understanding. 
Second, advanced techniques such as Gradient Boosting (e.g., XGBoost or LightGBM) or ensemble stacking could be tested to push performance beyond the Random Forest. 
Lastly, continuous retraining using new data collected over time will ensure the model adapts to changing environmental and operational conditions, 
maintaining its effectiveness as a sustainable, data-driven solution for water resource management in Tanzania.

 


