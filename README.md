## Assignment 11.1: What Drives the Price of a Car?

### **Goal**

The goal is to provide a reccomendation to used car dealership on what a consumer values in a used car. Perform a data analyisis and modeling to determine what are the factors that makes a car less or more expensive. 

### **Approach**

CRISP-DM Data Science lifecycle approach is applied. This process provides a framework for working through a data problem. 
The steps involved are following:

(1) Buisness understanding  
(2) Data understanding  
(3) Data preperation  
(4) Data modeling  
(5) Evaluation  
(6) Deployment  

#### **<ins>Business ojectives</ins>**  
The primary objective for used car dealership is to sell more cars, grow customer base and beat the competition in a business of selling used cars in their geographical region.

**Business success criterion** :


1.   Increase the customer churn
2.   Increase the used car business revenue by 25% YoY
3.   Become the #1 used car seller in the region

**Assess sitautaion** :


1.   Determine what customer values in a used car
2.   Understanding customer's spending to buy a used car

**Data mining and analyis goals** :


1.   To understand vaious categorical infomration that controls the used
car prices like:


*   Car's technical specifications
*   Geographical and demographics
*   Brand etc

#### **<ins>Data understanding</ins>** 

**Data**

Kaggle dataset is used containing information on 426K cars to ensure speed of processing.


1.   Accessing data file and loading in Pandas dataframe
2.   Examine, understand and describe the acquired data
3.   Identify mising data and irelevant data
4.   Verify data quality if it can help with business objectives


The atributes are detailed here :  

Data file at : 

**Data understanding report** :

1.   Size of acquired data = 426880 samples
2.   Data has total 18 categorical columns
3.   No duplicate samples

Most missing data are :


| Category | Missing  percentage|
|---|---|
| Size of vehicle | 71.7% |
| Cylinders | 41.6% |
|Condition | 40.7%|
| Drive | 30.5% |
|paint color | 30.5% |
| VIN | 37.7%|
| Type | 21.7% |

#### **<ins>Data preperation</ins>**

1.   Create a new data frame consists of cleaned and preprocessed data
2.   99.8 % of the samples having vechicle price < 100000 . Drop vehciles with prices > 1000000. these are price outliers
3.   Vehicles older than 100 years having high prices. Could be vintage vehicles.
4.   Vehicle price state and region wise is like white noise can be dropped
5.   id, VIN shoudl not influence the price, so shoudl be dropped
6.   Drop samples with odometer NA
7.   Drop the samples with year info as NA. Could not determine the age
8.   New feature 'age' is engineered from 'year' and dropped the year column
9.   More then 99% of the data has odometer reading < 300000. drop rest of the outliers


#### **<ins>Data modelling</ins>**

1.   Split the data in training and test set in 7:3
2.   Encode all categorical 'string' data types into numerical using JamesSteinEncoder()
3.   Encode 'condition' column using OrdinalEncoder
4.   Fill NA by 'missing' before encoding
5.   Create a pipeline for

     * Column transformer
     * StandardScalar
     * Ridge model

6. Use GridSearchCV with CV = 5 to tune the hyperparameters
7. Use alpha for Ridge regression [0.001, 1, 10, 100, 1000]
8. Use polynomial feature of degree 3

**Findings from the model evaluation**

* GridSearchCV with CV = 5 avoided overfitting and underfitting
* StandardScalar helped to remove biase by normalizing the values
* Polynomial feature with degree =3 reduced complexity with optimized mean squared error
* Ridge regression with alpha 0.001 found by GridSearchCV provded reduced model complexity  
 

#### **<ins>Deployment</ins>**  

### **Recommendations to the used car delears**

#### Based on data modelling and analysis, the top 3 parameters that drives the price of a car are

1.   **Car model**
2.   **Age of car - Older the car lesser the price**
3.   **Odometer - lesser the mileage , higher the price**


Following are the features that customers values most :

 |Parameters | Importance|
 |--|--|
|model |          0.524750|
|age     |        0.105356|
|odometer  |      0.046878|
|transmission  |  0.022941|
|fuel    |        0.016195|
|type    |        0.007739|
|drive   |        0.007094|
|title_status |   0.001929|
|manufacturer |   0.001692|
|paint_color  |   0.000744|
|size        |    0.000541|
|condition    |  -0.000012|