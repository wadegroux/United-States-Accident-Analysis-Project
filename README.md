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
To check for duplicate entries, I focus solely on the 'ID' column. The uniqueness of each entry is attributed to its ID number. Therefore, by crafting a query that groups rows based on the 'ID' column and counts the occurrences of each 'ID,' I can identify duplicates. The condition 'HAVING COUNT(*) > 1' filters out unique records, presenting only those with more than one occurrence.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/d89e247f-0dc8-4773-b734-9e81a3e1cd9b)

Upon execution, it was determined that there were no duplicate rows within the 'ID' column. This indicates that the dataset is devoid of any duplicate entries.

# Data Cleaning: Checking/Removing Outliers
I am going to check for outliers in columns Sunrise_Sunset, Severity, and Temperature_F. 

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/5addcd20-43a6-406c-8a14-d6e59e285307)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/03537099-12ec-4b93-ad16-e99f8c9e1bb2)

There were no outliers in these two columns.

To find outliers in the 'Temperature_F' column, I'll use the Interquartile Range (IQR) method by calculating the lower and upper thresholds based on the quartiles of the data. Values beyond these thresholds are considered outliers.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/5edc255a-637c-438c-8af5-38335032e2c1)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/deaf0ef0-b790-420c-886c-f4f426116f96)

I identified 3,332 rows of outliers using the IQR method. The outliers, mostly associated with extremely cold weather conditions, suggest a correlation between icy conditions and accidents. I've decided not to delete these outliers but will make a note for further analysis. Upon reviewing the data, the reported temperatures align with the corresponding states and cities, indicating accuracy.

Next, I will further examine the outliers within the identified 3,332 rows that are above 32 degrees. This step aims to determine if these specific outliers can provide valuable insights.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/285e050c-83c5-4656-be60-363eb7374942)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/37b6be7a-6234-44e9-8462-186149085cf5)
After this analysis, I found that out of the 3,332 outliers, only 5 had temperatures above 32 degrees. Removing these 5 outliers helps refine the dataset for a more accurate analysis. I will proceed to remove them and confirm the completion of this step.
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/95cdb05e-1a4b-4023-bb7d-c1aa6d23466d)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/d0978627-a298-4107-b7d5-39eff59a5553)

# Data Cleaning: Checking Data Types 
I will now ensure that the data types for my data table are correct. Note: I already did this when importing my dataset, but it never hurts to double-check.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/2ccd0b30-6ca4-4b35-a262-9d6154a3db39)

This allowed me to confirm, that my data types are correct.

# Data Cleaning: Validating Constraints
**Checking Unique Constraints**
Now, I will write a query that checks for duplicate records by comparing the total count of records with the count of unique values in the 'ID' column.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/204b695a-7749-44b2-8bb1-cf93c39ec8e1)

This allowed me to see that the counts are equal, indicating that there are no duplicate entries.

**Checking Primary Key Constraints**

I will now write a new query that checks for NULL values in the primary key column ('ID'). The result should be 0 NULL values. 

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/e4404ea5-f10b-4535-b302-5da174564bab)

 Result = 0 NULL VALUES FOUND

**Checking Consistency in 'STATE' and 'CITY' Columns** 
I will write a query that checks for NULL values in the state, and city columns. 

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/5d9ee9ef-722a-4199-af2a-068ab10f59c6)

The columns contained 0 NULL values. 

# Data Cleaning: Aggregate Functions For Summarization
**Counting Number Of Accidents Per State**
I will now write a query that counts the number of accidents for each state and displays the results in descending order.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/0a0fcb6f-f9f4-4d67-ad31-1e90ca5e9776)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/b04eff1c-c57c-418c-8ed2-0e5bbb4a0099)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/d135df95-1ccb-49aa-9657-00a89229c293)

NOTE: From examining these results, I need to consider that states with higher populations may skew the analysis. A higher population could lead to a higher probability of accidents occurring compared to states with lower populations.

**Calculating AVG Temperature For Each State**

I will write a query to calculate the average temperature for each state.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/324c1ec7-a8e2-4beb-9c2f-638019fd50bb)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/c9c7363f-634b-4852-839a-76234f27bfc7)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/004e09e5-b385-41fb-a74d-abc9ed39ecf1)

**Summarizing Severity Levels By State**

I will write a query to summarize severity levels (1-4) by state, providing the count of each severity level for every state. 

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/f8530da4-98d6-45af-916e-702148b97318)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/cc524409-6aad-400c-ae2d-b439799f017f)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/9f36b595-3bf7-4a60-b8df-08134d19098e)

**NOTE: The data opens up various possibilities for analysis, including the identification of high-severity areas, comparison of severity levels, trend analysis, correlation with weather conditions, geospatial visualization, safety recommendations, and evaluation of the impact of traffic management.**

# Data Cleaning: Review and Understand Data Distributions 
**Frequency Distribution of Severity Levels**

I will now write a query that shows how many accidents fall into each severity category(1-4).

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/9a88ac42-d486-4133-bc0c-3f2e6b3b808d)

Result: Shows me the distribution levels.

**Histogram of Temperature Distribution** 
I will create a query that generates a histogram, grouping temperature values into ranges and displaying the frequency of accidents in each range.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/24a1e80a-bef6-4081-8532-e74be9297f38)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/25bfe6d3-3b35-40a8-aef8-46e1600f42ed)

Result: Distribution of Severity Levels 

**Distribution of Day, Night, and Severity**
I will write a query that categorizes accidents based on the Sunrise_Sunset column. For each category, it will provide the total accident count as well as the severity levels 1-4. This way, I can analyze how severity is distributed during the day and night and identify periods with higher severity level accidents.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/fef1c5d7-dcf7-4bcb-87d4-0637cb5ef157)

Once I saw these results I wanted to find the results for severity count as percentages of each option day and night
To do this I am going to have to write a query that uses a Common Table Expression (CTE)


![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/bba19015-b7fb-4c13-b3a7-b5c1b08f1748)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/9b4aa8eb-dce7-4571-8c0a-fcba9579edaa)

After Seeing this I came to realize that the Severity Level 4 Percentage is higher at night than the day time even though the night only counts for 30.70% of accidents. This makes me think I might be able to prove my hypothesis that driving at night produces higher severity of wrecks.


















































