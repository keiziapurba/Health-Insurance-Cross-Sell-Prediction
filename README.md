# HEALTH INSURANCE CROSS SELL PREDICTION🚙🏥

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
|Age |Numerical| Age of the Customer.|
|Gender |Categorical|Gender of the Custome|
|Driving_License |Categorical|0 for customer not having DL, 1 for customer having DL.|
|Region_Code |Categorical|Unique code for the region of the customer.|
|Previously_Insured| Categorical | 0 for customer not having vehicle insurance, 1 for customer having vehicle insurance.|
|Vehicle_Age| Categorical | Age of the vehicle.|
|Vehicle_Damage | Categorical | Customer got his/her vehicle damaged in the past. 0 : Customer didn't get his/her vehicle damaged in the past.|
|Annual_Premium| Numerical| The amount customer needs to pay as premium in the year.|
|Policy_Sales_Channel| Categorical | Anonymized Code for the channel of outreaching to the customer ie. Different Agents, Over Mail, Over Phone, In Person, etc.|
|Vintage |Numerical|Number of Days, Customer has been associated with the company.|
|**Response** (Target Feature)| Categorical | 1 for Customer is interested, 0 for Customer is not interested.|


----

## Project Outline

### **- Observation**
- In this dataset, there are **no missing values**
- In this dataset, there are **no duplicate data**.
- There aren't columns that have odd summary values (min/mean/median/max/unique/top/freq) 

### **- Univariate Analysis**
Visualize every columns to gain insight.
- Skewed positif and bimodal: Age
- <img width="421" alt="Screen Shot 2022-03-08 at 13 41 57" src="https://user-images.githubusercontent.com/91368463/157181582-c3a81283-1563-4fb7-b717-6dd0bc0c5d9f.png">
- Outlier: Annual Premium
- <img width="444" alt="Screen Shot 2022-03-08 at 13 41 04" src="https://user-images.githubusercontent.com/91368463/157181466-2fd5007a-c588-494b-a7a1-0129f82e5a7f.png">
- Dominating value: Driving License
- Too many category: id, Region Code, Vintage, Annual Premium, Policy Sales Channel

### **- Multivariate Analysis**
Visualize correlation between features, in this case using correlation heatmap.
<img width="669" alt="Screen Shot 2022-03-08 at 13 38 30" src="https://user-images.githubusercontent.com/91368463/157181195-a9c6552b-527d-4c19-b660-799eb02725d1.png">

- Overall, correlations between features low, but there are 5 features that relevant to Response feature:
 1. Response - Vehicle Damage (0.35)
 2. Response - Previously Insured (0.34) 
 3. Response - Vehicle Age (0.22)
 4. Response - Policy Sales Channel (0.14)
 5. Response - Age (0.11)
- There is an interesting correlation between Response and Vehicle Damage feature. We will do Feature Encoding on these features, which is expected to produce performance that matches expectations. 

### **- Insight**
- Existing customers (Previously Insured) who already have vehicle insurance are 174628 customers. Customers who do not have vehicle insurance and are interested in having vehicle insurance are 46552 customers.
- Based on the distribution of customer age and vehicle age, age 24 is the majority of age for owning a vehicle with a vehicle age of less than 1 year.






### **- Preprocessing Data**
- There aren't missing values and no duplicate values.
- **Handling outliers** with a range in the form of IQR. Annual Premium data is the only data whose outliers are discarded because other data doesn't have outliers.

<img width="995" alt="Screen Shot 2022-03-08 at 13 15 47" src="https://user-images.githubusercontent.com/91368463/157178081-c983e3dc-4422-41fa-ac4d-148b2da3cb52.png">


### **- Feature Engineering**
- **Merge** the value of '> 2 Years' with the value '1-2 Years' to '> 1 Year'.

<img width="1001" alt="Screen Shot 2022-03-08 at 13 17 28" src="https://user-images.githubusercontent.com/91368463/157178244-087c6cc8-723a-4116-af9e-c4b96fa8ab9b.png">


Obtained the best engineering features occurred during one hot encoding + standardization + outliers handling and download sampling.

Here's the final result of the feature engineering:

- **Merge** the value of '> 2 Years' with the value '1-2 Years' to '> 1 Year' because the value of '> 2 Years' is far behind.
- Age and Vintage features are **standardized** with the StandardScaler() function. Annual Premium feature was **normalized** with the MinMaxScaler() function. Normalization is not used because it is more universal. This process needs to be done to overcome the column with a large value that will have a large effect on the results.
- Perform **encoding features** for Gender, Vehicle_Age, Region Code, Policy Sales Channel and Vehicle Damage features.
- **Change the data type** of Region_Code and Policy Sales Channel feature which was previously float data type to string for one hot encoding purposes.
- Doing **One Hot Encoding** of the Region_Code and Policy Sales Channel feature, then reduces it to top 5 classes.
- Perform **Class Imbalance handling** with **under_sampling** so that the total data is reduced from 300 thousand data to below 100 thousand data.


### **- Feature Transformation**
- Annual Premium was **normalized** with the normalization because the data was very large and so that it was normalized.
- Age and Vintage was **standarized** with standarization to bring down all the features to a common scale without distorting.


### **- Feature Encoding**
- Perform **label encoding** for Gender, Vehicle Age, and Vehicle Damage features using mapping to make new features with different label. 
- perform **one hot encoding** for Region Code and Policy Sales Channel.
- **Drop outdated column** from features engineering, features transformation, and features encoding. In this step we drop: ID, Vehicle Age, Gender, Region Code, Policy Sales Channel columns.
- Perform **Class Imbalance handling** with **under_sampling** so that the total data is reduced from 300 thousand data to below 100 thousand data.
<img width="381" alt="Screen Shot 2022-03-08 at 13 36 36" src="https://user-images.githubusercontent.com/91368463/157180877-dcfa3817-24e5-4a45-9b54-5e57a0c6086a.png">



-**Insight**
In the initial stage, all features are used and divide the features based on numeric types and categories. After performing Data Preprocessing, then the features are carried out by engineering features, transformation features, and encoding features. After all the processing, we found only a few features that have a high enough correlation.



### **- Modeling**
#### - Evaluation Metrics

We used **AUC (Area Under Curve)** metrics. We use AUC because it contains a Recall value that focuses on the True Positive Rate (True Positive and False Negative) and False Positive Rate. This is because this is a case of ranking problems which is very suitable to be implemented. The data is ranked based on the probability that people will take vehicle insurance. We also use **recall** because recall is suitable when we are concerned about the response rate ratio. The size of the response rate will reduce offering cost and will increase revenue due to the effectiveness of the sales team's offer.


### **- Modeling stage**
- In this stage we do modeling with 4 different models: Decision Tree, Logistic Regression, Random Forest, dan XGBoost and compare those models to pich the best model for tuning.
- In this modeling stage, first, we split the Train & Test data. Then we conducted several model experiments, including Naive Bayes, Decision Tree, Logistic Regression, Random Forest, XGBoost and Extra Tree Classifier. Of the four models, we have chosen two, which are Random Forest and XGBoost because they have high recall and AUC values, and aren't overfit.

<img width="534" alt="Screen Shot 2022-03-08 at 13 29 24" src="https://user-images.githubusercontent.com/91368463/157179961-7028db46-1d5b-41e1-a3bc-bf70077fd6e0.png">


#### **- Hyperparameter tuning**
Of the two models we chose, the model that we think is the best-fit is the XGBoost model because the AUC value is higher than Random Forest, with an AUC score of 85%. Hyperparameters tuning used for the model are max_depth=3, learning_rate=0.1, eta=0.005, gamma=0.0, min_child_weight=5, colsample_bytree=0.7.

<img width="998" alt="Screen Shot 2022-03-08 at 13 27 53" src="https://user-images.githubusercontent.com/91368463/157179755-2dd54a1c-c170-4100-9c8d-626e4474d0ec.png">


#### **- Importance Feature**
After interpreting the model, the most important feature is Vehicle Damage followed by Previously Insured, Email Marketing, Telephone, and Age.

<img width="748" alt="Screen Shot 2022-03-08 at 13 31 36" src="https://user-images.githubusercontent.com/91368463/157180211-6c65e327-a024-43ad-bfd6-1ec4c08723ab.png">


#### **- Business Insight & Recommendation**
- After modeling, it can be predicted that the average response rate will increase by 56%.
- Rae Bareli (Region 28) had a significant increase of 76%, as it reached customers who could potentially experience vehicle damage as many as 70,236 cases.
- This model can also predict the current revenue for region 28 from 64,172,574 to 259,187,797 with normal premiums. By increasing the annual premium to 5000 per month (previously 3222), we can predict the expected revenue in the 28 region to be 402,215,700.
- Total revenue of the region (regions 28, 8, 29, 41, 46) was 589,971,909 with a reduction in expenditure of 803,400. Overall we expect revenue of 589,168,509. The estimated revenue includes costs for approaching customers to subscribe to vehicle insurance via email marketing, telephone, and youtube ads.

<img width="830" alt="Screen Shot 2022-03-08 at 13 33 34" src="https://user-images.githubusercontent.com/91368463/157180527-3728e47e-ffae-4557-b78b-3370a91d3c3d.png">

<img width="1052" alt="Screen Shot 2022-03-08 at 13 33 58" src="https://user-images.githubusercontent.com/91368463/157180537-2e90ba22-483e-41ab-b6fb-c0a33222f2d7.png">



