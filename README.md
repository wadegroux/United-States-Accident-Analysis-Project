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

1. **Hotspot Identification:**
   - Can we pinpoint high-accident areas and understand contributing factors for targeted prevention?

2. **Environmental Impact:**
   - How do weather conditions correlate with accident occurrence and severity?

3. **Accident Severity Analysis:**
   - What factors most significantly influence the severity of accidents?

## Data Sourcing
The dataset is sourced from Kaggle, titled "US-Accidents," and provided by Sobhan Moosavi, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Rajiv Ramnath, and Radu Teodorescu. Their work, "A Countrywide Traffic Accident Dataset" (2019), and the associated paper provide valuable insights.

### Citations
- Moosavi, Sobhan, et al. "A Countrywide Traffic Accident Dataset," 2019.
- Moosavi, Sobhan, et al. "Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights."

# Data Exploration: Checking for Missing Values

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

# Data Exploration: Checking/Removing Outliers
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

# Exploration: Validating Constraints
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

# Data Exploration: Aggregate Functions For Summarization
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

# Data Exploration: Review and Understand Data Distributions 
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

Once I saw these results, I wanted to calculate the severity count as percentages for each option, day and night. To achieve this, I will write a query that utilizes a Common Table Expression (CTE).


![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/bba19015-b7fb-4c13-b3a7-b5c1b08f1748)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/9b4aa8eb-dce7-4571-8c0a-fcba9579edaa)

After seeing the new results, I realized that the Severity Level 4 percentage is higher at night than during the daytime, even though the night only accounts for 30.70% of accidents. This leads me to consider that I might be able to substantiate my hypothesis that driving at night contributes to higher severity of accidents.

# Data Exploration: Continued (EDA)

I will review any available data dictionary or metadata that describes the variables.

The only variable I need to understand more is the "Weather Condition." I can create a query to retrieve all unique values from this column.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/a0360859-f6bb-4a5f-96dc-234b527f4062)

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/1fc61755-868a-434c-a429-43d0af5873b9) ![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/402f1728-247a-4115-ae28-0c73d7d6d673) ![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/229ebced-a197-425e-a085-1bd78e4d1c36) ![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/dffd5425-7641-472f-bbb4-3fc6c22e7e49)

After reviewing this, I plan to summarize it to simplify my analysis process, reducing the number of unique variables in the columns. I will utilize the 'CASE' statement to generate a new column with summarized categories for the 'Weather Condition' column.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/f7c66109-aa51-46fd-bf60-cfe7a27e97b2)

SIDE NOTE: THIS TOOK FOREVER!
Following the execution of this operation, the new column has been successfully created. To ensure the accuracy of all values, I will verify the uniqueness of values in the weather category column.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/3f32f681-6154-443a-9c13-9004577a22c3)

The reduction from 107 different variables to 10 in the weather condition category significantly simplifies the data, making it more conducive to analysis and extraction of insights.

I will now write a query that calculates the total number of accidents, the count for each severity level, and the percentage of accidents for each severity level within each weather category. It then orders the results by the total number of accidents in descending order.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/bdbc778e-dd55-4feb-9a13-4967a6199891)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/3e87207e-d4b2-4a24-a447-03a850bac388)

I need a new query that returns the top 5 weather conditions with the highest severity percentage in Severity 2-4 levels, excluding clear and cloudy conditions. This analysis will help me understand the impact of weather conditions on accidents and severity levels.

This shows that now has the highest Severity Level 4 Percentage

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/1370d65d-fe1a-470b-80b7-1d17cfb4aa18)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/2a8f45b4-5cd1-4bf1-911b-03b29589fd22)

This tells me the relationships of accidents by each weather condition and how there is a relationship with weather that has an influences higher severity level.

**Identify High Accident Areas by State**
To pinpoint high-accident areas and understand contributing factors by state, I need to perform analysis based on the states considering factors such as accident counts severity levels and weather conditions.

First I will write a query that allow me to Identify High-Accident Areas by State
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/6c4f91d3-fa76-4f78-ab58-0bd3c82717ad)

**Explore Weather Conditions by State**
I will now write a query that provides a breakdown of severity levels for each state 
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/fef9f2fc-e803-4772-9ecc-6f2d8d99e467)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/6655a350-262c-46ae-b123-84d81085cd02)


I will now combine the previous 3 query's to get a holistic view of high-accident areas, severity levels, and contributing factors by state. I only want to see the top 10 for my analysis.

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/e97d0194-1db4-4537-beb8-81c4d489240d)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/e697ee29-bd5d-45f8-96cd-776ada0f5b00)
![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/9170b1d9-241e-4578-85b0-ef25a47dc0ed)

I can use this newly created table for my data visualization. This will allow me to identify high accident areas and understand contributing factors for targeted prevention. By analyzing the accident data, I can see patterns, trends, and commonalities in terms of locations, types of accidents, and contributing factors. 

After being able to visualize this information for targeted prevention we could use Consider using machine learning models to predict accident hotspots based on historical data. These models can identify key features contributing to accidents. Another option is Work with local authorities, traffic safety organizations, or law enforcement to gain additional insights and collaborate on targeted prevention initiatives.

Exciting news! Having laid a solid foundation with the data, I'm now taking the next step using Tableau to craft a compelling narrative. 

# Data Visualizations: Crafting Creative Data Visualizations
You can interact with the Tableau Dashboard Here: https://public.tableau.com/app/profile/wade.groux/viz/USAccidentsPortfolioProject/Dashboard1 

![image](https://github.com/wadegroux/United-States-Accident-Analysis-Project/assets/157087862/809d210e-f167-439e-b946-171df28b9c6f)

In my Tableau Analysis Visualization, I've developed an interactive dashboard for the United States Traffic Accidents Severity Analysis, featuring:

• Geographical mapping of accidents and total accident count.

• Segmentation of accidents by severity levels.

• Analysis of accidents in relation to different weather conditions.

• Distinction between accidents occurring during the day and night.

• Customizable filters for states, time of day, severity levels, and weather categories.

• A comprehensive exploration of the interplay between these factors, providing insights into the determinants of accident severity in the United States.

# Data Analysis: Insights and Recommendations

# Insights:

• Daytime accidents exhibited a higher severity level compared to nighttime accidents, suggesting that there might be specific factors contributing to increased severity during daylight hours.

• Incidents occurring in adverse weather conditions such as rain, snow, and fog resulted in a higher severity level, particularly in the serious condition category, when contrasted with clear and cloudy weather. This indicates a correlation between challenging weather conditions and elevated accident severity.

• Geographical analysis revealed that the eastern part of the United States experienced a higher volume of accidents than the western region. This observation might be attributed to the higher population density in the eastern states, potentially leading to increased traffic and a greater likelihood of accidents.
	
• Analysis of accidents by severity level indicated that a significant proportion of accidents fell into the "minor" category. Further investigation into the specific factors contributing to minor accidents could provide insights into preventive measures to reduce overall accident rates.
	
• When examining accidents by state, it became evident that certain states consistently showed higher severity levels across different weather conditions and times of the day. This suggests the presence of state-specific factors or road conditions that may contribute to the increased severity of accidents, warranting a closer look into localized safety measures.

# Recommendations:
	
• Daytime Safety Measures: Implement targeted safety measures during daytime hours, considering the observed higher severity of accidents during this period. This could include enhanced visibility measures, increased law enforcement presence, and public awareness campaigns emphasizing safe driving practices during daylight.

• Weather-Responsive Traffic Management: Develop weather-responsive traffic management strategies, especially during rain, snow, and fog. This may involve deploying weather-specific road maintenance crews, updating signage for adverse conditions, and implementing technology-driven alerts to drivers when severe weather is anticipated.

• Eastern States Safety Initiatives: Given the higher accident rates in the eastern part of the United States, collaborate with states in this region to develop and implement region-specific safety initiatives. These could include targeted educational programs, improved infrastructure, and stricter law enforcement to address the unique challenges contributing to the higher accident volume.

• Focus on Minor Accidents: Devote attention to understanding and preventing minor accidents, as they constitute a significant portion of incidents. Investigate the specific causes behind these minor accidents and introduce preventive measures, such as driver education campaigns or road design improvements, to reduce their occurrence.

• State-Specific Safety Plans: Work with states showing consistently higher severity levels across different conditions to develop state-specific safety plans. These plans could involve a combination of targeted enforcement, infrastructure improvements, and community engagement to address the localized factors contributing to elevated accident severity.
























































