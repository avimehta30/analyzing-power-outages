# Analyzing Power Outages 🔌
Project for DSC80 UCSD
by Christian Guerra and Avi Mehta

## Introduction
In this project, my team and I analyzed a dataset containing the power outages throughout various states in the United States. The dataset provides comprehensive information on the outages, including details about their causes, durations, and the geographical, climatic, and economic characteristics of the affected areas. Additionally, the dataset includes data on electricity consumption patterns and land-use characteristics, offering a rich context for our analysis.

## Data Cleaning and Exploratory Data Analysis

### Data Cleaning and Preprocessing
We prepared the dataset by addressing missing values, converting data types, and creating new derived features such as combining date and time information into datetime columns.

## Data Description
The original raw dataset contains 1534 rows, corresponding to 1534 outages, and 57 columns. For the purpose of our analysis, we focused on the following columns:

| Columns | Description |
| ------- | ----------- |
| 'OUTAGE.DURATION' | Duration of outage events (in minutes) |
| 'CUSTOMERS.AFFECTED'| Number of customers affected by the power outage event |
| 'ANOMALY.LEVEL' | Gravity of natural disaster on power outage |
| 'CLIMATE.REGION' | U.S. Climate regions as specified by National Centers for Environmental Information |
| 'CAUSE.CATEGORY' | Categories of all the events causing the major power outages |
| 'NERC.REGION' | North American Electric Reliability Corporation (NERC) regions involved in the outage event |

### Cleaned Data Example
Here is an example of the cleaned dataset:

| OUTAGE_START_DATETIME | OUTAGE_RESTORATION_DATETIME | NERC.REGION | CUSTOMERS.AFFECTED | OUTAGE.DURATION | CLIMATE.REGION | CAUSE.CATEGORY | ANOMALY.LEVEL |
| --------------------- | --------------------------- | ----------- | ------------------ | --------------- | -------------- | -------------- | ------------ |
| 2011-07-01 17:00:00   | 2011-07-03 20:00:00         | MRO         | 70000.000000       | 3060.0          | East North Central | severe weather | -0.3          |
| 2014-05-11 18:38:00   | 2014-05-11 18:39:00         | MRO         | 143456.222731      | 1.0             | East North Central | intentional attack | -0.1          |
| 2010-10-26 20:00:00   | 2010-10-28 22:00:00         | MRO         | 70000.000000       | 3000.0          | East North Central | severe weather | -1.5          |
| 2012-06-19 04:30:00   | 2012-06-20 23:00:00         | MRO         | 68200.000000       | 2550.0          | East North Central | severe weather | -0.1          |
| 2015-07-18 02:00:00   | 2015-07-19 07:00:00         | MRO         | 250000.000000      | 1740.0          | East North Central | severe weather | 1.2           |



### Exploratory Data Analysis (EDA)
We conducted EDA to understand the distribution and characteristics of the outages, visualizing the data to identify key trends and patterns.

#### Univariate Analysis
Look at the distributions of relevant columns separately by using DataFrame operations and drawing at least two relevant plots.
<iframe
  src="assets/climate_region_distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Bivariate Analysis
Look at the statistics of pairs of columns to identify possible associations. For instance, you may create scatter plots and plot conditional distributions, or box-plots. You must plot at least two such plots in your notebook. The results of your bivariate analyses will be helpful in identifying interesting hypothesis tests!

<iframe
  src="assets/outage_duration_vs_customers_affected.html.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

#### Interesting Aggregates
Choose columns to group and pivot by and examine aggregate statistics. Embed at least one grouped table or pivot table in your website and explain its significance.

| CLIMATE.REGION     | Amount of Outages | Average Length of Outage Duration |
|--------------------|-------------------|-----------------------------------|
| Central            | 166               | 1424.870996                       |
| East North Central | 110               | 2666.067258                       |
| Northeast          | 296               | 1394.343880                       |
| Northwest          | 125               | 1004.585496                       |
| South              | 190               | 1211.802011                       |


## Assessment of Missingness

### NMAR Analysis
To determine whether data are likely NMAR (Not Missing At Random), we must reason about the data-generating process. In our dataset, if the missingness of the `OUTAGE.DURATION` is due to factors not recorded in the dataset, such as manual errors during data entry or specific reporting practices of certain regions, it could be NMAR. However, we cannot conclude this solely by looking at the data. Additional information about the data collection process would be necessary to determine NMAR.

### Missingness Dependency
We analyzed the dependency of the missingness of the `OUTAGE.DURATION` column on other columns in the dataset by performing permutation tests.

### Missingness Summary

| Column                      | Missingness Proportion |
|-----------------------------|------------------------|
| OUTAGE_START_DATETIME       | 0.005867               |
| OUTAGE_RESTORATION_DATETIME | 0.037810               |
| NERC.REGION                 | 0.000000               |
| CUSTOMERS.AFFECTED          | 0.288787               |
| OUTAGE.DURATION             | 0.037810               |
| CLIMATE.REGION              | 0.003911               |
| CAUSE.CATEGORY              | 0.000000               |
| ANOMALY.LEVEL               | 0.005867               |
| MONTH                       | 0.005867               |
| OUTAGE_DURATION_MISSING     | 0.000000               |

### Permutation Test Results
#### Categorical Column: CAUSE.CATEGORY
- Observed Statistic: 0.2520091580226147
- P-value: 0.0

#### Categorical Column: CLIMATE.REGION
- Observed Statistic: 0.2535212947392274
- P-value: 0.004

#### Categorical Column: NERC.REGION
- Observed Statistic: 0.3153910849453322
- P-value: 0.0

#### Categorical Column: ANOMALY.LEVEL
- Observed Statistic: 0.4918007853547923
- P-value: 0.0

#### Categorical Column: MONTH
- Observed Statistic: 0.22267850229522704
- P-value: 0.118

### Interpretation
The p-values obtained from the permutation tests indicate that the missingness of the `OUTAGE.DURATION` column is dependent on `CAUSE.CATEGORY`, `CLIMATE.REGION`, `NERC.REGION`, and `ANOMALY.LEVEL` (p-value < 0.05). However, the missingness of `OUTAGE.DURATION` is not dependent on `MONTH` (p-value = 0.118).

### Detailed Analysis
#### MONTH
The p-value of 0.118 for the `MONTH` column suggests that the missingness of `OUTAGE.DURATION` is not significantly dependent on the month in which the outage occurred. This implies that the occurrence of missing data for outage duration does not vary significantly across different months. The permutation test's observed statistic for `MONTH` fell within the distribution of the permuted statistics, indicating no strong relationship between `MONTH` and missingness in `OUTAGE.DURATION`.

#### CLIMATE.REGION
On the other hand, the `CLIMATE.REGION` column shows a significant dependency on the missingness of `OUTAGE.DURATION` with a p-value of 0.004. This indicates that the missing data for outage duration is not uniformly distributed across different climate regions. The observed statistic for `CLIMATE.REGION` is significantly higher than most of the permuted statistics, suggesting that certain climate regions may have more or less missing data, possibly due to varying reporting standards or environmental factors affecting data collection.

### Graphs
#### Permutation Test: MONTH and Missingness of OUTAGE_DURATION
The following plot shows the distribution of test statistics from the permutation test for the `MONTH` column. The red dashed line represents the observed test statistic.

<iframe src="assets/permutation_test_month.html" width="800" height="600" frameborder="0"></iframe>

#### Permutation Test: CAUSE.CATEGORY and Missingness of OUTAGE_DURATION
The following plot shows the distribution of test statistics from the permutation test for the `CAUSE.CATEGORY` column. The red dashed line represents the observed test statistic.

<iframe src="assets/permutation_test_cause.html" width="800" height="600" frameborder="0"></iframe>

## Hypothesis Testing
We formulated and tested hypotheses to explore the relationship between various factors and the duration of power outages. Specifically, we examined how climate regions might affect outage durations.

## Modeling and Prediction
Finally, we explored predictive modeling to identify the most important causes and characteristics of major power outages. The goal was to build a model that can predict the cause of an outage based on given conditions, which can help energy companies implement preventative measures.

