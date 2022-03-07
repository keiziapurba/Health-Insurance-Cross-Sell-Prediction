# HEALTH INSURANCE CROSS SELL PREDICTION🚙🏥
Predicting whether a customer would be interested in buying Vehicle Insurance so that the company can then accordingly plan its communication strategy to reach out to those customers and optimise its business model and revenue.


---

## Table of Content
  * [Background](#background)
    - [Business Domain](#business-domain)
    - [Problem Statement](#problem-statement)
    - [Business Metrics](#business-metrics)
    - [Goals](#goals)
    - [Objective](#objective)
    - [Predictive Analytics](#predictive-analytics)
  * [Data Description](#data-description)
  * [Project Outline](#project-outline)
    - [Observation](#observation)
    - [Univariate Analysis](#univariate-analysis)
    - [Multivariate Analysis](#multivariate-analysis)
    - [Insight](#insight)
    - [Preprocessing Data](#preprocessing-data)
    - [Feature Engineering](#feature-engineering)
    - [Feature Transformation](#feature-transformation)
    - [Feature Encoding](#feature-encoding)
    - [Modeling](#modeling)
    - [Business Insight & Recommendation](#business-insight-&-recommendation)

---


## **Background**
Our client is an Insurance company that has provided Health Insurance to its customers now they need your help in building a model to predict whether the policyholders (customers) from past year will also be interested in Vehicle Insurance provided by the company.

An insurance policy is an arrangement by which a company undertakes to provide a guarantee of compensation for specified loss, damage, illness, or death in return for the payment of a specified premium. A premium is a sum of money that the customer needs to pay regularly to an insurance company for this guarantee.

*Building a model to predict whether a customer would be interested in Vehicle Insurance is extremely helpful for the company because it can then accordingly plan its communication strategy to reach out to those customers and optimize its business model and revenue.*

#### **Business Domain**: Vehicle Insurance

#### **Problem Statement**: How to predict whether a health insurance owner will be interested in vehicle insurance with the most efficient approach?

#### **Business Metrics**: Revenue and Response Rate

#### **Goals**: Predict customers interest who owns health insurance in Vehicle Insurance to increase Revenue, Conversion Rate, and number of customers


#### **Objective**: Build a model to predict whether health insurance owners will be interested in vehicle insurance from data from health insurance owners and their responses. Also, using an automatic bidding system model for customers who subscribe to health insurance in order to get information about vehicle insurance.

#### **Predictive Analytics**: Creating a model that can help predict whether customers, including those who will be interested in vehicle insurance or not


### **Data Description**
Dataset contains information about demographics (gender, age, region code type), Vehicles (Vehicle Age, Damage), Policy (Premium, sourcing channel) etc. related to a person who is interested in vehicle insurance. (https://www.kaggle.com/anmolkumar/health-insurance-cross-sell-prediction)
Total data points: 381109 


| Feature Name | Type | Description |
|----|----|----|
|id| (continous) |Unique identifier for the Customer.|
|Age |(continous)| Age of the Customer.|
|Gender |(dichotomous)|Gender of the Custome|
|Driving_License |(dichotomous)|0 for customer not having DL, 1 for customer having DL.|
|Region_Code |(nominal)|Unique code for the region of the customer.|
|Previously_Insured| (dichotomous)| 0 for customer not having vehicle insurance, 1 for customer having vehicle insurance.|
|Vehicle_Age| (nominal)| Age of the vehicle.|
|Vehicle_Damage | (dichotomous)| Customer got his/her vehicle damaged in the past. 0 : Customer didn't get his/her vehicle damaged in the past.|
|Annual_Premium| (continous)| The amount customer needs to pay as premium in the year.|
|Policy_Sales_Channel| (nominal)| Anonymized Code for the channel of outreaching to the customer ie. Different Agents, Over Mail, Over Phone, In Person, etc.|
|Vintage |(continous)|Number of Days, Customer has been associated with the company.|
|**Response** (Dependent Feature)|(dichotomous)| 1 for Customer is interested, 0 for Customer is not interested.|


----

## Project Outline

### **- Observation**
- In this dataset, there are **no missing values**
- In this dataset, there are **no duplicate data**.
- There aren't columns that have odd summary values (min/mean/median/max/unique/top/freq) 

### **- Univariate Analysis**
Visualize every columns to gain insight.
- Skewed positif and bimodal: Age
- Outlier: Annual Premium
- Dominating value: Driving License
- Too many category: id, Region Code, Vintage, Annual Premium, Policy Sales Channel

### **- Multivariate Analysis**
Visualize correlation between features, in this case using correlation heatmap.
- Overall, correlations between features low, but there are 5 features that relevant to Response feature:
 1. Response - Vehicle Damage (0.35)
 2. Response - Previously Insured (0.34) 
 3. Response - Vehicle Age (0.22)
 4. Response - Policy Sales Channel (0.14)
 5. Response - Age (0.11)
- There is an interesting correlation between Response and Vehicle Damage feature. We will do One Hot Encoding on these features, which is expected to produce performance that matches expectations. 

### **- Insight**
- Existing customers (Previously Insured) who already have vehicle insurance are 174628 customers. Customers who do not have vehicle insurance and are interested in having vehicle insurance are 46552 customers.
- Based on the distribution of customer age and vehicle age, age 24 is the majority of age for owning a vehicle with a vehicle age of less than 1 year.



### **- Preprocessing Data**
- There aren't missing values and no duplicate values.
- **Handling outliers** with a range in the form of IQR. Annual Premium data is the only data whose outliers are discarded because other data doesn't have outliers.

### **- Feature Engineering**
- **Merge** the value of '> 2 Years' with the value '1-2 Years' to '> 1 Year'.

Obtained the best engineering features occurred during one hot encoding + standardization + outliers handling and download sampling.

Here's the final result of the feature engineering:

- **Merge** the value of '> 2 Years' with the value '1-2 Years' to '> 1 Year' because the value of '> 2 Years' is far behind (lame).
- Age, Annual_Premium, Policy_Sales_Channel, and Vintage features are **standardized** with the StandardScaler () function. Normalization is not used because it is more universal. This process needs to be done to overcome the column with a large value that will have a large effect on the results.
- Perform **encoding features** for Gender, Vehicle_Age, and Vehicle Damage features using pandas' get_dummies function. The encoding process uses the drop_first = True parameter because there are only 2 columns that are correlated with one another.
- **Change the data type** of Region_Code feature which was previously float data type to string for binary encoding purposes.
- Doing **BinaryEncoding** of the Region_Code feature which has a unique value of 53 to 7 classes then reduces it to 6 classes because one feature is only worth 0. One hot is not used because this method will generate 53 new columns.
- Perform **Class Imbalance handling** with **under_sampling** so that the total data is reduced from 300 thousand data to below 100 thousand data.


### **- Feature Transformation**
- Annual Premium was **normalized** with the normalization because the data was very large and so that it was normalized.
- Age and Vintage was **standarized** with standarization to bring down all the features to a common scale without distorting.


### **- Feature Encoding**
- Perform **label encoding** for Gender, Vehicle Age, and Vehicle Damage features using mapping to make new features with different label. 
- perform **one hot encoding** for Region Code and Policy Sales Channel.
- **Drop outdated column** from features engineering, features transformation, and features encoding. In this step we drop: ID, Vehicle Age, Gender, Region Code, Policy Sales Channel columns.
- Perform **Class Imbalance handling** with **under_sampling** so that the total data is reduced from 300 thousand data to below 100 thousand data.

-**Insight**
In the initial stage, all features are used and divide the features based on numeric types and categories. After performing Data Preprocessing, then the features are carried out by engineering features, transformation features, and encoding features. After all the processing, we found only a few features that have a high enough correlation.



### **- Modeling**
#### - Evaluation Metrics

We used **AUC (Area Under Curve)** metrics. We use AUC because it contains a Recall value that focuses on the True Positive Rate (True Positive and False Negative) and False Positive Rate. This is because this is a case of ranking problems which is very suitable to be implemented. The data is ranked based on the probability that people will take vehicle insurance. We also use **recall** because recall is suitable when we are concerned about the response rate ratio. The size of the response rate will reduce offering cost and will increase revenue due to the effectiveness of the sales team's offer.


### **- Modeling stage**
In this stage we do modeling with 4 different models: Decision Tree, Logistic Regression, Random Forest, dan XGBoost and compare those models to pich the best model for tuning.

In this modeling stage, first, we split the Train & Test data. Then we conducted several model experiments, including Naive Bayes, Decision Tree, Logistic Regression, Random Forest, XGBoost and Extra Tree Classifier. Of the four models, we have chosen two, which are Random Forest and XGBoost because they have high recall and AUC values, and aren't overfit.

#### **- Hyperparameter tuning**
Of the two models we chose, the model that we think is the best-fit is the XGBoost model because the AUC value is higher than Random Forest, with an AUC score of 85%. Hyperparameters tuning used for the model are max_depth=3, learning_rate=0.1, eta=0.005, gamma=0.0, min_child_weight=5, colsample_bytree=0.7.


#### **- Importance Feature**
After interpreting the model, the most important feature is Vehicle Damage followed by Previously Insured, Email Marketing, Phone, and Age.


#### **- Business Insight & Recommendation**
- After modeling, it can be predicted that the average response rate will increase by 56%.
- Rae Bareli (Region 28) had a significant increase of 76%, as it reached customers who could potentially experience vehicle damage as many as 70,236 cases.
- This model can also predict the current revenue for region 28 from 64,172,574 to 259,187,797 with normal premiums. By increasing the annual premium to 5000 per month (previously 3222), we can predict the expected revenue in the 28 region to be 402,215,700.
- Total revenue of the region (regions 28, 8, 29, 41, 46) was 589,971,909 with a reduction in expenditure of 803,400. Overall we expect revenue of 589,168,509. The estimated revenue includes costs for approaching customers to subscribe to vehicle insurance via email marketing, telephone, and youtube ads.





