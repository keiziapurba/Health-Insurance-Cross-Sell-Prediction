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
    - [Business Insight](#business-insight)
    - [Preprocessing Data](#preprocessing-data)
    - [Feature Engineering](#feature-engineering)
    - [Feature Transformation](#feature-transformation)
    - [Feature Encoding](#feature-encoding)
    - [Modeling](#modeling)
  * [Reccomendation](#reccomendation)
  * [Reference](#reference)

---


## **Background**
Our client is an Insurance company that has provided Health Insurance to its customers now they need your help in building a model to predict whether the policyholders (customers) from past year will also be interested in Vehicle Insurance provided by the company.

An insurance policy is an arrangement by which a company undertakes to provide a guarantee of compensation for specified loss, damage, illness, or death in return for the payment of a specified premium. A premium is a sum of money that the customer needs to pay regularly to an insurance company for this guarantee.

*Building a model to predict whether a customer would be interested in Vehicle Insurance is extremely helpful for the company because it can then accordingly plan its communication strategy to reach out to those customers and optimize its business model and revenue.*

#### **Business Domain**: Vehicle Insurance

#### **Problem Statement**: How to predict whether a health insurance owner will be interested in vehicle insurance with the most efficient approach?

#### **Business Metrics**: Revenue and Conversion Rate

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

### **- Business Insight**
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
- Perform **label encoding** for Gender, Vehicle_Age, and Vehicle Damage features using mapping to make new features with different label. 
- **Drop outdated column** from features engineering, features transformation, and features encoding. In this step we drop: Vehicle Age, Vehicle Damage, Gender, Age, Annual Premium, Vintage columns.
- Perform **Class Imbalance handling** with **under_sampling** so that the total data is reduced from 300 thousand data to below 100 thousand data.

-**Insight**
In the initial stage, all features are used and divide the features based on numeric types and categories. After performing Data Preprocessing, then the features are carried out by engineering features, transformation features, and encoding features. After all the processing, we found only a few features that have a high enough correlation. The following features will be used and dropped:


a. Features that we used:
   - Vehicle Damage (Yes)
   - Previously Insured
   - Vehicle Age (> 1 Year)
   - Age (standarization)
   - Annual Premiun (normalization)

b. Features that we dropped:
   - id
   - Age 
   - Vintage 
   - Annual Premium




### **- Modeling**
#### - Evaluation Metrics

**The AUC (Area Under Curve)** metrics are used. This is because this is a case of ranking problems which is very suitable to be implemented. The data is ranked based on the probability that people will take vehicle insurance.

We also use **precision** because precision is suitable when we are concerned about the win rate / customer conversion ratio. The size of the winrate will reduce offering cost and will increase revenue due to the effectiveness of the sales team's offer.
The greater the value of the precision produced by the model means the more likely it is to find people who will actually take out vehicle insurance.

### **- Modeling stage**

### **- Determine the baseline model**

The determination process is done by using **RandomizedSearch** for Hyperparameter tuning in the algorithm: *Logistic Regression, KNN, NB, ANN, Decision Tree, Random Forest, XGBoost, AdaBoost*.

<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/persen.png"  width="400" height="300">
</p>

Full feature engineering is used at this stage.
Based on precision and AUC values. Then the chosen model is XGBoost

#### **- Hyperparameter tuning**
After obtaining the best engineering features, hyperparameter tuning was performed again
<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Hyperparameter%20Tuning.png"  width="400" height="300">
</p>


#### **- Cross-validation**
StratifiedKfolds (with k = 10) are used to ensure the distribution of each class in the train and validation is the same
<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Cross%20Validation.png"  width="700" height="300">
</p>


#### **- Importance Feature**
From the results of a more in-depth analysis of feature importance, we can find out that people who tend to take out vehicle insurance are people who:
- the vehicle was damaged before
- Never took out vehicle insurance before
- the age of the vehicle more than one year.

<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Feature%20Importance.png"  width="400" height="300">
</p>

### **- Recommendation**
Use the proposed model to predict potential customer
Focusing marketing in Region Code 28 (Tamil Nadu) by adding more store or join an exhibition
Reach people who are 30-62 years of age by giving any promotion / dicsount for millennials, and easy apply to x generation
Reach out to people who have damaged their car and old car age by collaborating with second hand dealer and garage






# **Prediction of Cross Sales of Health Insurance 🏠 🏥** #
## ***"Made as a final project task at Rakamin Data Science Bootcamp"*** ##
**by: Robertsen Putra Sugianto**

### **- Background**

India roughly accounts for only about 1% of the global vehicle population. However, it accounts for about 6% of total global road accidents 
1. Based on reports from insurance regulators in India in 2018 the vehicle (motorbike) insurance business increased by 8.91% 
2. As an insurance company that has developed data on health insurance owners, it is hoped that this data can be used for the vehicle insurance business. In the process of developing a vehicle insurance business, building a model to predict whether health insurance users will be interested or not.

**Business Domain**: Vehicle Insurance

**Problem**: How to predict whether a health insurance owner will be interested in vehicle insurance?

**Business Metrics**: Number of health insurance customers who use Vehicle Insurance, Revenue, and Win Rate

**Goals**: Predict the interest of health insurance owners in Vehicle Insurance to increase Revenue, Win Rate, and number of customers

**Objective**: Build a model to predict whether health insurance owners will be interested in vehicle insurance from data from health insurance owners and their responses.

**Predictive Analytics**: Creating a model that can help predict whether customers, including those who will be interested in vehicle insurance or not


### **- Dataset**
<p align="center">
<img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Dataset.png"  width="400" height="300">
</p>

- The datasets needed in making this model can be obtained from **the internal record of Health Insurance owner data** which contains customer data including Demographics (Gender, Age, Region Code), Vehicles (Vehicle Age, Vehicle Damage), Policy (Annual Premium, Policy Sales Channel). ), etc. ***(https://www.kaggle.com/anmolkumar/health-insurance-cross-sell-prediction)***

- This dataset has a total of **12 columns**, 381,109 rows of data, and no data is lost. With **3 columns of which are categorical** (Gender, Vehicle_Age, Vehicle_Damage), and the remaining **8 columns are numeric**.
- In general, there is no statistically strange data, with the exception of the Annual_Premium column which has a very large maximum value and is very different from the minimum value.
- There are quite a lot of **outliers** for the Annual_Premium column, with quite a large number and a long way off
- The Age distribution is **Positively Skewed**. The response is also quite **imbalanced**
- Vehicle_Damage has a fairly balanced data distribution. Meanwhile, Vehicle_Age is quite lame, with the category value> 2 Years far behind the others.


### **- Insight**
<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Insight%20-%20Win%20Rate%20before.png"  width="400" height="300">
</p>
<p>
  <em>People whose vehicles have been damaged have the potential to take out insurance. The bad experience someone has about their vehicle breaking makes them think about taking out insurance</em>
 </p>


<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Insight%20-%20Vehicle%20Age.png"  width="400" height="300">
</p>
<p>
  <em>Customers with older vehicles are also more interested in vehicle insurance than customers with younger vehicle ages</em>
 </p>


<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Insight%20-%20Region%20Code.png"  width="400" height="300">
</p>
<p>
  <em>People in Region Code 28 are a suitable target to increase the number of customers, as many are attracted to vehicle insurance offers, far more than other regions.The number of people who insure their vehicles in Region 28 (Tamil Nadu), is because people in Region 28 have their vehicles damaged.</em>
 </p>


<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Insight%20-%20Age.png"  width="400" height="300">
</p>
<p>
  <em>Potential buyers are in the age range of 30 to 62 years</em>
 </p>

### **- Preprocessing Data**
- In this dataset, there are **no missing values**
- In this dataset, there are **no duplicate data**.
- The data of Annual Premium was **normalized** with the log function because the data was very large and so that it was normalized.
- **Detect and remove outliers** with a range in the form of IQR. Annual Premium data is data whose outliers are discarded because other data does not have outliers

### **- Feature Engineering**

Iterates feature engineering on the model
Feature iterations that are done:
One Hot Encoding only (imbalance)
One Hot Encoding + Outliers Handling (imbalance)
One Hot Encoding (oversampling)
One Hot Encoding (undersampling)
One Hot Encoding + standardization + outliers handling (undersampling)

Obtained the best engineering features occurred during one hot encoding + standardization + outliers handling and download sampling.

Here's the final result of the feature engineering:

- **Merge** the value of '> 2 Years' with the value '1-2 Years' to '> 1 Year' because the value of '> 2 Years' is far behind (lame).
- Age, Annual_Premium, Policy_Sales_Channel, and Vintage features are **standardized** with the StandardScaler () function. Normalization is not used because it is more universal. This process needs to be done to overcome the column with a large value that will have a large effect on the results.
- Perform **encoding features** for Gender, Vehicle_Age, and Vehicle Damage features using pandas' get_dummies function. The encoding process uses the drop_first = True parameter because there are only 2 columns that are correlated with one another.
- **Change the data type** of Region_Code feature which was previously float data type to string for binary encoding purposes.
- Doing **BinaryEncoding** of the Region_Code feature which has a unique value of 53 to 7 classes then reduces it to 6 classes because one feature is only worth 0. One hot is not used because this method will generate 53 new columns.
- Perform **Class Imbalance handling** with **under_sampling** so that the total data is reduced from 300 thousand data to below 100 thousand data.


### **- Modeling**
#### - Evaluation Metrics

**The AUC (Area Under Curve)** metrics are used. This is because this is a case of ranking problems which is very suitable to be implemented. The data is ranked based on the probability that people will take vehicle insurance.

We also use **precision** because precision is suitable when we are concerned about the win rate / customer conversion ratio. The size of the winrate will reduce offering cost and will increase revenue due to the effectiveness of the sales team's offer.
The greater the value of the precision produced by the model means the more likely it is to find people who will actually take out vehicle insurance.

### **- Modeling stage**

### **- Determine the baseline model**

The determination process is done by using **RandomizedSearch** for Hyperparameter tuning in the algorithm: *Logistic Regression, KNN, NB, ANN, Decision Tree, Random Forest, XGBoost, AdaBoost*.

<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/persen.png"  width="400" height="300">
</p>

Full feature engineering is used at this stage.
Based on precision and AUC values. Then the chosen model is XGBoost

#### **- Hyperparameter tuning**
After obtaining the best engineering features, hyperparameter tuning was performed again
<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Hyperparameter%20Tuning.png"  width="400" height="300">
</p>


#### **- Cross-validation**
StratifiedKfolds (with k = 10) are used to ensure the distribution of each class in the train and validation is the same
<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Cross%20Validation.png"  width="700" height="300">
</p>


#### **- Importance Feature**
From the results of a more in-depth analysis of feature importance, we can find out that people who tend to take out vehicle insurance are people who:
- the vehicle was damaged before
- Never took out vehicle insurance before
- the age of the vehicle more than one year.

<p align="center">
  <img src="https://github.com/robertsenputras/DS-HealthInsuranceCrossSelling/blob/master/fig/Feature%20Importance.png"  width="400" height="300">
</p>

### **- Recommendation**
Use the proposed model to predict potential customer
Focusing marketing in Region Code 28 (Tamil Nadu) by adding more store or join an exhibition
Reach people who are 30-62 years of age by giving any promotion / dicsount for millennials, and easy apply to x generation
Reach out to people who have damaged their car and old car age by collaborating with second hand dealer and garage
