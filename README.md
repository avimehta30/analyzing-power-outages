# Analyzing Power Outages
Project for DSC80 UCSD
by Christian Guerra and Avi Mehta

# Introduction 
In this project my team and I analyzed a data set containing the power outages throughout various states in the United States. The dataset provides comprehensive information on the outages, including details about their causes, durations, and the geographical, climatic, and economic characteristics of the affected areas. Additionally, the dataset includes data on electricity consumption patterns and land-use characteristics, offering a rich context for our analysis. 

# Index:

## Data Cleaning and Preprocessing: 
We prepared the dataset by addressing missing values, converting data types, and creating new derived features such as combining date and time information into datetime columns.

## Exploratory Data Analysis (EDA):
We conducted EDA to understand the distribution and characteristics of the outages, visualizing the data to identify key trends and patterns.

## Missingness Analysis: 
We analyzed the mechanisms and dependencies of missing data within the dataset. This involved performing permutation tests to determine if the missingness was related to other variables.

## Hypothesis Testing: 
We formulated and tested hypotheses to explore the relationship between various factors and the duration of power outages. Specifically, we examined how climate regions might affect outage durations.

## Modeling and Prediction: 
Finally, we explored predictive modeling to identify the most important causes and characteristics of major power outages. The goal was to build a model that can predict the cause of an outage based on given conditions, which can help energy companies implement preventative measures.


The original raw dataset contains 1534 rows, corresponding to 1534 outages, and 57 columns. For the purpose of our analysis, we focused on the following columns:

| Columns| Description |
| ----------- | ----------- |
| 'OUTAGE.DURATION' | Duration of outage events (in minutes) |
| 'CUSTOMERS.AFFECTED'| Number of customers affected by the power outage event|
| 'ANOMALY.LEVEL'| Gravity of natural disaster on power outage|
| 'CLIMATE.REGION'| U.S. Climate regions as specified by National Centers for Environmental Information|
| 'CAUSE.CATEGORY'| Categories of all the events causing the major power outages|
| 'NERC.REGION'| North American Electric Reliability Corporation (NERC) regions involved in the outage event |


## Data Cleaning Process 

To ensure the dataset is ready for analysis, we performed several data cleaning steps. Below is an explanation of how we cleaned the data:

## Loading and Initial Cleaning: 
We began by loading the dataset and addressing initial inconsistencies:

## Loading the Dataset: 
We opened the power outages dataset while skipping the first 5 rows, which contain metadata rather than actual data.
Handling Missing Values: We replaced "NA" values with NaN to standardize missing value representation.

We then performed mean imputation on numerical columns and filled the mode for categorical columns. We combined the date and time columns into datetime columns and dropped the original columns to remove redundancy. The clean dataset looks like this:

| OUTAGE_START_DATETIME | OUTAGE_RESTORATION_DATETIME | NERC.REGION | CUSTOMERS.AFFECTED | OUTAGE.DURATION | CLIMATE.REGION | CAUSE.CATEGORY | ANOMALY.LEVEL |
|-----------------------|-----------------------------|-------------|-------------------|-----------------|----------------|----------------|---------------|
| 2011-07-01 17:00:00   | 2011-07-03 20:00:00         | MRO         | 70000.000000      | 3060.0          | East North Central | severe weather  | -0.3          |
| 2014-05-11 18:38:00   | 2014-05-11 18:39:00         | MRO         | 143456.222731     | 1.0             | East North Central | intentional attack | -0.1          |
| 2010-10-26 20:00:00   | 2010-10-28 22:00:00         | MRO         | 70000.000000      | 3000.0          | East North Central | severe weather  | -1.5          |
| 2012-06-19 04:30:00   | 2012-06-20 23:00:00         | MRO         | 68200.000000      | 2550.0          | East North Central | severe weather  | -0.1          |
| 2015-07-18 02:00:00   | 2015-07-19 07:00:00         | MRO         | 250000.000000     | 1740.0          | East North Central | severe weather  | 1.2           |


## Exploratory Data Analysis

First, I wanted to see how the number of outages has changed over time.
<iframe
  src="assets/outage_over_time.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I also wanted to see the distribution of major causes of power outages.
<iframe
  src="assets/major_causes.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Next, I wanted to understand the distribution of climate regions affected by power outages.
<iframe
  src="https://github.com/chguerra15/analyzing-power-outage/blob/main/climate_region_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


I also analyzed the relationship between outage duration and the number of customers affected.
<iframe
  src="assets/outage_duration_vs_customers.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Finally, I created a pivot table to explore the average outage duration and the number of outages per climate region.

| CLIMATE.REGION | Amount of Outages | Average Length of Outage Duration |
|----------------|-------------------|-----------------------------------|
| East North Central | 200 | 1440.5 |
| Southeast | 300 | 1500.7 |
| West | 150 | 1300.2 |

