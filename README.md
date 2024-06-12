# Analyzing Power Outages
Project for DSC80 UCSD
by Christian Guerra and Avi Mehta

# Introduction 
In this project my team and I analyzed a data set containting the power oputages throughout varius states in the United States. The dataset provides comprehensive information on the outages, including details about their causes, durations, and the geographical, climatic, and economic characteristics of the affected areas. Additionally, the dataset includes data on electricity consumption patterns and land-use characteristics, offering a rich context for our analysis. 

##Index:

##Data Cleaning and Preprocessing: We prepared the dataset by addressing missing values, converting data types, and creating new derived features such as combining date and time information into datetime columns.

##Exploratory Data Analysis (EDA): We conducted EDA to understand the distribution and characteristics of the outages, visualizing the data to identify key trends and patterns.

##Missingness Analysis: We analyzed the mechanisms and dependencies of missing data within the dataset. This involved performing permutation tests to determine if the missingness was related to other variables.

##Hypothesis Testing: We formulated and tested hypotheses to explore the relationship between various factors and the duration of power outages. Specifically, we examined how climate regions might affect outage durations.

##Modeling and Prediction: Finally, we explored predictive modeling to identify the most important causes and characteristics of major power outages. The goal was to build a model that can predict the cause of an outage based on given conditions, which can help energy companies implement preventative measures.


##The original raw dataset contains 1534 rows, corresponding to 1534 outages, and 57 columns. For the purpose of our analysis, we focused on the following columns:

| Columns| Description |
| ----------- | ----------- |
| OUTAGE.DURATION | Duration of outage events (in minutes) |
| CUSTOMERS.AFFECTED| Number of customers affected by the power outage event|
| ANOMALY.LEVEL| Gravity of natural disaster on power outage|
| CLIMATE.REGION| U.S. Climate regions as specified by National Centers for Environmental Information|
| CAUSE.CATEGORY| Categories of all the events causing the major power outages|
| NERC.REGION| North American Electric Reliability Corporation (NERC) regions involved in the outage event |


#Data Cleaning Process 

To ensure the dataset is ready for analysis, we performed several data cleaning steps. Below is an explanation of how we cleaned the data:

##Loading and Initial Cleaning: 
We began by loading the dataset and addressing initial inconsistencies:

##Loading the Dataset: 
We opened the power outages dataset while skipping the first 5 rows, which contain metadata rather than actual data.
Handling Missing Values: We replaced "NA" values with NaN to standardize missing value representation.

