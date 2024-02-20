# United States Accident Analysis Project

![iStock-1408564727](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/22064b95-3b37-4150-8290-e9deebfb0ea5)

## Introduction
This project demonstrates my proficiency in data analysis using a substantial dataset sourced from Kaggle. The dataset covers US traffic accidents from February 2016 to March 2023, and my analysis involves critical thinking, meticulous data cleaning, thorough analysis, and effective visualization. SQL was used for initial cleaning, followed by detailed visual analysis in Tableau.

**Note:** The problem statement and objectives were generated using ChatGPT as an illustrative example to showcase my analytical skills for my portfolio.

## Problem Statement
The project delves into the US-Accidents dataset, spanning 49 states and collected from multiple Traffic APIs. The objective is to gain insights into car accidents, enabling real-time prediction, hotspot identification, environmental impact analysis, and severity assessment.

## Objective
Conduct an in-depth analysis of the US-Accidents dataset to unravel patterns contributing to a holistic understanding of car accidents.

## Questions To Be Answered During Analysis
1. **Temporal Patterns:**
   - Are there identifiable trends in seasonal variations in accident rates over the dataset period?

2. **Hotspot Identification:**
   - Can we pinpoint high-accident areas and understand contributing factors for targeted prevention?

3. **Environmental Impact:**
   - How do weather conditions correlate with accident occurrence and severity?

4. **Accident Severity Analysis:**
   - What factors most significantly influence the severity of accidents?

## Data Sourcing
The dataset is sourced from Kaggle, titled "US-Accidents," and provided by Sobhan Moosavi, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Rajiv Ramnath, and Radu Teodorescu. Their work, "A Countrywide Traffic Accident Dataset" (2019), and the associated paper provide valuable insights.

### Citations
- Moosavi, Sobhan, et al. "A Countrywide Traffic Accident Dataset," 2019.
- Moosavi, Sobhan, et al. "Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights."

# Data Cleaning: Checking for Missing Values

## Overview
This section outlines the process of checking for missing values in the dataset ('us_accidents_data') using dynamic SQL. Identifying missing values is a crucial step in ensuring the integrity and completeness of the dataset.

I created a query that would return the total number of missing values for each column the dynamic script generates all columns in the specified table ('us_Accidents_data'). It uses 'INFORMATION_SCHEMA.COLUMNS' view to fetch the column names and constructs the query accordingly. Using this is a lot faster than typing in multiple different blocks. I found that there were missing values from the columns Temperature_F, Weather_Condition, and Sunrise_Sunset.
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/65e8900d-db2d-4615-a602-65459243bef1)
![Missing Value Counts](https://github.com/wadegroux/United-States-Accident-Analysis-Project/blob/main/Screenshot%202024-02-18%20234158.png)
![Missing Value Counts](https://github.com/wadegroux/United-States-Accident-Analysis-Project/blob/main/Screenshot%202024-02-18%20234330.png)

I ended up deleting all of the rows that had missing values.
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/8b5de333-b944-4e8c-a0b6-8fbd1abb3e99)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/f38bcc70-cfdc-477f-935e-2c37046ce161)

After the rows had been deleted I went and double checked to insure that all of the missing values were equal to 0

# Data Cleaning: Checking/Removing Duplicates
To check for duplicate entries the only column I need to pay attention to is 'ID' this is due to the fact that the ID number is unique to each entry so if there are any duplicates it will be shown here. To do this I need to write a query that groups the rows by the 'ID' column and counts the occurrences of each 'ID'. The 'HAVING COUNT(*) > 1' condition filters out unique records, showing only those with one occurrence.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/d89e247f-0dc8-4773-b734-9e81a3e1cd9b)

After executing this there were 0 rows within the ID column that were duplicates, meaning that my data is free from duplicate entries.

# Data Cleaning: Checking/Removing Outliers
I am going to check for outliers in columns Sunrise_Sunset, Severity, and Temperature_F. 

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/5addcd20-43a6-406c-8a14-d6e59e285307)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/03537099-12ec-4b93-ad16-e99f8c9e1bb2)

There were no outliers in these two columns

Now for Temperature_F column to identify the outliers first I am going to need to find the threshold within the column and to do that I am going to use the Interquartile Range (IQR) method.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/5edc255a-637c-438c-8af5-38335032e2c1)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/deaf0ef0-b790-420c-886c-f4f426116f96)

This allowed me to find 3,332 Rows of outliers. The majority of these were due to extremely cold weather conditions which would help me derive an insight that Icey conditions lead to wrecks I will not delete these but, I am making note of it to come back later. While looking at the data with the States and Cities these temperatures reported seemed accurate. The data aligns with the locations.

Next, I am going to find the outliers that are within those outliers that are above 32 degrees to see if the outlier is actually something that can be turned into an insight.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/285e050c-83c5-4656-be60-363eb7374942)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/37b6be7a-6234-44e9-8462-186149085cf5)
After doing this I was able to discover that there were only 5 out of the 3332 outliers that I found. Which is cool. By finding the outliers I was able to find the outliers within those that applied to my analysis.
I will now remove those 5 I found. And verify that it is completed.
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/95cdb05e-1a4b-4023-bb7d-c1aa6d23466d)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/d0978627-a298-4107-b7d5-39eff59a5553)

# Data Cleaning: Checking Data Types 
I will now insure that the data tyoes for my data table are correct. NOTE: I already did this when importing my data set but, never hurts to double check.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/2ccd0b30-6ca4-4b35-a262-9d6154a3db39)

This allowed me to confirm that my data types are correct.





















