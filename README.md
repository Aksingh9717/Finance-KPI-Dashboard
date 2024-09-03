# FINANCE KPI DASHBOARD

Dashboard snapshot :- ![Screenshot 2024-09-03 224721](https://github.com/user-attachments/assets/91d642ad-ade9-4a6e-885c-bb3ea3e63598)


## Problem Statement:
In a highly competitive market, companies must track and analyze their sales performance to make informed strategic decisions. This project demonstrates how to build a comprehensive Power BI dashboard to visualize and analyze sales performance data, enabling management to monitor key metrics, identify trends, and make data-driven decisions.

## Project Workflow:
### 1. Data Preparation:
Source: The data is provided in an Excel format.

Power BI Integration:
Load the data into Power BI.

Use Power Query Editor to clean and transform the data.

Ensure that the headers are correctly set as the first row.
Unpivot other columns in the "Actual" and "Targets" tables for normalization.

### 2. Data Modelling:
Create relationships between tables:- 
Connect the Calendar table to the Actual table via the Date column using a many-to-one relationship.

This setup is crucial for the accuracy and flexibility of your DAX calculations and visualizations.

### 3. DAX Calculations:
Here are the DAX calculations used to drive the insights in the dashboard:


#### 1.Total Sales Actual: 
    SUM(Actual[Sales])
#### 2.Total Sales Target: 
    SUM(Targets[Sales])
#### 3.Variance: 
    Total sales target - Total sales actual
#### 4.Variance %: 
    DIVIDE([Variance],[Total sales target])
#### 5.YTD Sales Actual: 
    CALCULATE([Total sales actual],DATESYTD('Calendar'[Date].[Date]))
#### 6.YTD Variance: 
    YTD sales target - YTD sales actual
#### 7.YTD Variance %: 
    DIVIDE([YTD variance],[YTD sales target])

#### 8.YTD Sales Target: 
    CALCULATE([Total Sales Target],DATESYTD('Calendar'[Date]))
#### 9.Months Target Reached: Count of months where targets were met.
    VAR months_with_target_reached = FILTER(ALL('Calendar'), [Variance] > 0)
    RETURN COUNTROWS(months_with_target_reached)
#### 10.Trend Chart Title: Dynamic title displaying the number of months targets were met.
    VAR month_count = COUNTROWS('Calendar')
    RETURN "We met targets for " & [Months Target Reached] & " out of " & month_count
#### 11.Target Status: Binary indicator of whether the target was met.
    IF([Variance] > 0, 1, -1)
#### 12.Variance Pct Label:Shows the variance percentage with an emoji indicator.
    VAR up = "🟢"
    VAR down = "🔴"
    VAR formatted_var_pct = FORMAT(ABS([Variance %]),"0.0%")
    RETURN formatted_var_pct & " " & IF([Variance %] > 0, up, down)


### 4. Dashboard Design:
The dashboard is designed with several critical visual components:

#### KPIs:
Displays key metrics like Total Sales Actual, Total Sales Target, Variance, and YTD Variance.

Helps the management quickly grasp performance insights.

#### Column Chart:
Compares actual sales against target sales over time.

A dynamic header reflects the current status of target achievements.

#### Sales Performance Table:
Lists individual salesperson performance with images.

Includes metrics like Actual Sales, Target Sales, and Variance %.

A sparkline shows trends for each individual.

#### Slicer:
Allows filtering by team for more focused analysis.

#### Smart Narrative:
Provides automatically generated insights and explanations based on the data presented in the dashboard.

### 5. Insights and Conclusions:
#### Performance Overview: The dashboard reveals that the team met sales targets in 12 out of 14 months, showcasing a strong overall performance.
#### Trends: Both Total Sales Actual and Total Sales Target have shown a downward trend in recent months, requiring strategic intervention.

 #### Actionable Insights: The variance percentage and YTD variance indicate areas where performance can be improved, enabling management to focus efforts on underperforming segments.

This project serves as a practical example of how to leverage Power BI for sales performance analysis, providing critical insights that drive business decisions. The detailed steps and visualizations included in the repository will be beneficial for those looking to understand the power of data analytics and visualization in a business context.


#### Dashboard snapshot :-
 ![Screenshot 2024-09-03 233240](https://github.com/user-attachments/assets/92ae1095-e8f7-4fb2-bdb5-5a07194a2f3f)


![Screenshot 2024-09-03 233308](https://github.com/user-attachments/assets/264d8f08-33ea-4fe5-905f-e7b4f846f805)
