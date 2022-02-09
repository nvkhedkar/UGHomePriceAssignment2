# House Price Prediction Assignment
House price model creation using regularization


## Table of Contents
* [General Info](#general-information)
* [Technologies Used](#technologies-used)
* [Assumptions](#assumptions)
* [Derived Features](#derived-features)
* [Conclusions](#conclusions)
* [Acknowledgements](#acknowledgements)

<!-- You can include any other section that is pertinent to your problem -->

## General Information
A US-based housing company named Surprise Housing has decided to enter the Australian market. The company uses data analytics to purchase houses at a price below their actual values and flip them on at a higher price.  
The company is looking at prospective properties to buy to enter the market.  
The company wants to know:
- Which variables are significant in predicting the price of a house, and
- How well those variables describe the price of a house.

<!-- You don't have to answer all the questions - just the ones relevant to your project. -->
## Assumptions
Total number of features after creating dummy variables = 232  
We did not drop multi-correlated features in the beginning because: 
1. Lasso performs feature selection  

2. Ridge will drive down values of bad features towards zeo 

3. We wanted to see how badly Linear regression performs with 
    1. Many features some of which are multi-correlated 

We use __Robust scaling__, because some variables are skewed and Robust Scaling has less effect of outliers.  
We performed __log transformation__ on __SalePrice__ because it is skewed.  
We used __Stratified sampling with a dummy variable__ to create train/test sets, because even after log transform there was a slight skew.  

## Derived Features

|Feature|Description|Formula|
|---|---|---|
|Age|Age of the property|2022 - YearBuilt|
|RemodAge|How long ago the property was remodeled|2022 - YearRemodAdd|
|GarageAge|How old the garage is|2022 - GarageYrBlt|    
__The feature "Age" turned out to be a top 5 predictor in Lasso as will be seen.__  
## Conclusions
- Optimal alpha values
    - Lasso: 0.001
    - Ridge: 15

|Model|alpha|features|r2_train|r2_test|mse_train|mse_test|
|---|---|---|---|---|---|---|
|Linear|-|230|0.9523|0.8415|0.0070|0.0217|
|Ridge|15.0000|228|0.9340|0.9034|0.0097|0.0132|
|Lasso|0.0010|69|0.9237|0.9004|0.0112|0.0136|

We will recommend Lasso model to the customer:
- It has only 69 features. This will make it easy to explain and interpret. 
- It explains 90.04% of the variability based on test Adjusted R-squared.
- Adjusted R2-square is comparable to ridge. But ridge uses 228 features. So it is more complex. 
- Linear regression is overfitting – Adjusted R2-sqaured are 0.95 (train) and 0.84 (test)  

The top 10 features:
|Feature Name|Coefficient|Interpretation|
|---|---|---|
|GrLivArea|0.1668|Larger houses will get higher price|
|OverallQual|0.1284|Better Quality property will get higher price
|SaleType_New|0.1013|Newer home will get higher price|
|Neighborhood_Crawfor|0.0989|Crawford neighborhood will get higher price|
|Age|-0.0858|New homes will get higher price|
|Neighborhood_Somerst|0.0697|Somerset neighborhood will get higher price|
|MSZoning_RL|0.0609|Homes in Residential Low Density areas will get higher price|
|SaleCondition_Normal|0.0520|If Sale condition is normal the home will get higher price
|BsmtFinSF1|0.0520|High Type 1 finished square feet gives high prices|
|TotalBsmtSF|0.0520|Larger basements give higher prices|

## Bonus - RFE explored
- Finally rfe is explored. Features are reduced to 100 using RFE. 
- After reducing features, Linear, Ridge and Lasso are compared.
- Lasso again does well and eleminates more variables. 

## Technologies Used
- Python:     3.9.6
- pandas:     1.3.2
- numpy:      1.21.2
- sklearn:    1.0.1
- seaborn:    0.11.2
- matplotlib: 3.4.3


<!-- As the libraries versions keep on changing, it is recommended to mention the version of library used in this project -->

## Contact
Created by [@nvkhedkar] - feel free to contact me!


<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->