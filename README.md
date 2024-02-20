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











