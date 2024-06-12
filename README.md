# Analyzing Power Outages
**Project for DSC80 UCSD**  
**by Christian Guerra and Avi Mehta**

## Introduction 
In this project, my team and I analyzed a dataset containing the power outages throughout various states in the United States. The dataset provides comprehensive information on the outages, including details about their causes, durations, and the geographical, climatic, and economic characteristics of the affected areas. Additionally, the dataset includes data on electricity consumption patterns and land-use characteristics, offering a rich context for our analysis. 

## Index:

### Data Cleaning and Preprocessing: 
We prepared the dataset by addressing missing values, converting data types, and creating new derived features such as combining date and time information into datetime columns.

### Exploratory Data Analysis (EDA):
We conducted EDA to understand the distribution and characteristics of the outages, visualizing the data to identify key trends and patterns.

### Missingness Analysis: 
We analyzed the mechanisms and dependencies of missing data within the dataset. This involved performing permutation tests to determine if the missingness was related to other variables.

### Hypothesis Testing: 
We formulated and tested hypotheses to explore the relationship between various factors and the duration of power outages. Specifically, we examined how climate regions might affect outage durations.

### Modeling and Prediction: 
Finally, we explored predictive modeling to identify the most important causes and characteristics of major power outages. The goal was to build a model that can predict the cause of an outage based on given conditions, which can help energy companies implement preventative measures.

The original raw dataset contains 1534 rows, corresponding to 1534 outages, and 57 columns. For the purpose of our analysis, we focused on the following columns:

| Columns              | Description                                                                           |
|---------------------|---------------------------------------------------------------------------------------|
| `OUTAGE.DURATION`   | Duration of outage events (in minutes)                                                |
| `CUSTOMERS.AFFECTED`| Number of customers affected by the power outage event                                |
| `ANOMALY.LEVEL`     | Gravity of natural disaster on power outage                                           |
| `CLIMATE.REGION`    | U.S. Climate regions as specified by National Centers for Environmental Information   |
| `CAUSE.CATEGORY`    | Categories of all the events causing the major power outages                          |
| `NERC.REGION`       | North American Electric Reliability Corporation (NERC) regions involved in the outage event |

## Data Cleaning Process 

To ensure the dataset is ready for analysis, we performed several data cleaning steps. Below is an explanation of how we cleaned the data:

### Loading and Initial Cleaning: 
We began by loading the dataset and addressing initial inconsistencies:
- **Loading the Dataset**: We opened the power outages dataset while skipping the first 5 rows, which contain metadata rather than actual data.
- **Handling Missing Values**: We replaced "NA" values with NaN to standardize missing value representation.

### Imputation of Missing Values
To deal with missing values in both numerical and categorical columns, we used different imputation strategies:
- **Mean Imputation for Numerical Columns**: For numerical columns (`OUTAGE.DURATION`, `CUSTOMERS.AFFECTED`, and `ANOMALY.LEVEL`), we replaced missing values with the mean of the respective columns.
- **Mode Imputation for Categorical Columns**: For categorical columns (`CLIMATE.REGION`, `CAUSE.CATEGORY`, and `NERC.REGION`), we replaced missing values with the mode (most frequent value) of the respective columns.

### Creating Datetime Columns
To facilitate time-based analysis, we combined separate date and time columns into single datetime columns:
- **Combining `OUTAGE.START.DATE` and `OUTAGE.START.TIME`**: We created a new column `OUTAGE_START_DATETIME` by combining the outage start date and time.
- **Combining `OUTAGE.RESTORATION.DATE` and `OUTAGE.RESTORATION.TIME`**: We created a new column `OUTAGE_RESTORATION_DATETIME` by combining the outage restoration date and time.

### Dropping Redundant Columns
After creating the datetime columns, we dropped the original date and time columns to avoid redundancy and maintain a clean dataset.

### Selecting Relevant Columns
Finally, we selected a subset of columns that are relevant to our analysis, focusing on key variables related to the outages and their characteristics.

### Cleaned Dataset Preview
The cleaned dataset looks like this:

| OUTAGE_START_DATETIME | OUTAGE_RESTORATION_DATETIME | NERC.REGION | CUSTOMERS.AFFECTED | OUTAGE.DURATION | CLIMATE.REGION      | CAUSE.CATEGORY    | ANOMALY.LEVEL |
|-----------------------|-----------------------------|-------------|--------------------|-----------------|---------------------|-------------------|---------------|
| 2011-07-01 17:00:00   | 2011-07-03 20:00:00         | MRO         | 70000.000000       | 3060.0          | East North Central  | severe weather    | -0.3          |
| 2014-05-11 18:38:00   | 2014-05-11 18:39:00         | MRO         | 143456.222731      | 1.0             | East North Central  | intentional attack| -0.1          |
| 2010-10-26 20:00:00   | 2010-10-28 22:00:00         | MRO         | 70000.000000       | 3000.0          | East North Central  | severe weather    | -1.5          |
| 2012-06-19 04:30:00   | 2012-06-20 23:00:00         | MRO         | 68200.000000       | 2550.0          | East North Central  | severe weather    | -0.1          |
| 2015-07-18 02:00:00   | 2015-07-19 07:00:00         | MRO         | 250000.000000      | 1740.0          | East North Central  | severe weather    | 1.2           |

By following these steps, we ensured that the dataset was clean, consistent, and ready for further analysis and visualization.

