# Mental-Health-Analysis
Employed females in the Unites States


## Project Overview

This data analysis project aims to provide insight into the Factors that affect mental Health. By analayzing the work interest data, we seek to identify trends and make data-driven recommendations to help respondents grow their interest in work.

We will be able to answer key questions, such as:

- Do self employed females have a higher work interest ratio than non self employed females?
- Do females with a mental health history have a lower work interest?
- What occupation has the highest work interest?

### Data Sources
Mental Health Dataset
This dataset records a global survey conducted to track trends in mental health. The data covers a range of variables such as levels of stress, depression, anxiety, subjective well-being, and use of mental health services. The survey involved respondents from various demographic backgrounds, including gender, employment status, and geographic region. This dataset aims to provide a better understanding of changes in mental health globally over the specified time period.

With million of apps around nowadays, the following data set has become very key to getting top trending apps in iOS app store. This data set contains more than 7000 Apple iOS mobile application details. The data was extracted from the iTunes Search API at the Apple Inc website. R and linux web scraping tools were used for this study.

### Tools
- SQL - Data Analysis

### Exploratory Data Analysis

EDA involved exploring the app data to understand the characteristics of the data, structure, and reveals issue in the dataset. These issues can include missing values and outliers. 

In the initial data EDA phase, we performerd the following tasks:

- Check for any missing values in key fields
- Identify biases
- Get an overview of the respondents background

### Data Cleaning/Preparation

In the initial data preparation phase, we performed the following tasks:
1. Data loading and inspection
2. Handling missing values
3. Data cleaning and formatting

### Data Analysis
  
  (Some interesting code/features worked with)

``` SQL  
--Determine wether respondents with mental health history have higher work interest than those without mental health history

SELECT
    History_type,
    AVG(WorkInterestCount) AS Interest
FROM (
    SELECT
        CASE
            WHEN Mental_Health_History = 'Yes' THEN 'History'
            ELSE 'NoHistory'  
        END AS History_type,
        COUNT(Work_Interest) AS WorkInterestCount
    FROM
        portfolioproject.dbo.[Mental Health Analysis]
    GROUP BY
        Mental_Health_History, Work_Interest
) AS Subquery
GROUP BY
    History_type;

-- Determine if there more respondents with a mental health history and no work interest seeking treatment

SELECT
    treatment_type,
    SUM(TotalFemales) AS TotalFemales
FROM (
    SELECT
        CASE
            WHEN Treatment = 'Yes' THEN 'YesTreatment'
            ELSE 'NoTreatment'
        END AS treatment_type,
        COUNT(gender) AS TotalFemales
    FROM
        portfolioproject.dbo.[Mental Health Analysis]
    WHERE
        Mental_Health_History = 'Yes'
		AND Work_Interest = 'No'
    GROUP BY
        work_interest, Treatment, Mental_Health_History, gender
) AS Subquery
GROUP BY
    treatment_type;
```

### Results/Findings

The analysis results are summarized as follow:
1. Females who are both self employed and not self employed have lower work interest
2. Females with no mental health history have higher work interest than females with mental history
3. There are more females with no work interest and a mental health history seeking treatment than those who aren't
4. Females who are housewives have the highest work interest

### Recommendations

Based on the analysis, we recommend the following actions:
- Conduct another survey to understand why females who are seeking treatment still don't have an interest in work
- Discover other variables such as occupation, work culture, and personal life that impact their interest in work
- Discover what the respondents like and dislike about their job

### Limitations

- I had to modify the original dataset to only include females because there was a larger population of males in the dataset
- I chose to focus on the United States
- I couldn't strictly compare those who were self employed to non self employed because there was a larger amount of respondents who were not self employed

### References

1.  [Kaggle Dataset]([https://www.kaggle.com/datasets/ramamet4/app-store-apple-data-set-10k-apps](https://www.kaggle.com/datasets/divaniazzahra/mental-health-dataset))
