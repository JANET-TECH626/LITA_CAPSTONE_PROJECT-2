# LITA_CAPSTONE_PROJECT-2
This repository contains my final project 2 as a newbie Data Analyst, showing my skills in data analysis, visualization, and insights extraction.


### PROJECT TITLE: CUSTOMER SEGMENTATION OF A SUBSCRIPTION SERVICE

[PROJECT OVERVIEW](#project-overview)

[DATA SOURCES](#data-sources)

[DATA DESCRIPTION](#data-description)

[TOOLS USED](#tools-used)

[DATA CLEANING AND PREPARATIONS](#data-cleaning-and-preparations)

[EXPLORATORY DATA ANALYSIS](#exploratory-data-analysis)

[DATA ANALYSIS](#data-analysis)

[DATA VISUALIZATION](#data-visualization)


### PROJECT OVERVIEW
---
This project involves the analysis o customer's data for a subscription service to identify segments and trends. This project aims at understanding customers behaviour, track subscription types and idetifying ket trends in cancellations snd renewals. the final deliverables is a Power BI dashboard to present the analysis.
 
### DATA SOURCES
---
Data used for this project was an excel data provided by the Incubator Hub LITA facilitators, the data was converted to CSV format, before importing to SQL, for easy and seamless analysis. 

### DATA DESCRIPTION
---
The dataset includes the following fields:
1. Customer ID: Unique identifier givemn to each customers
2. Customer Name: Names of the customers
3. Region: Regions subscriptions were made from
4. Subscription Type: Type of Subscription package done bu the customers
5. Subscription Start: Date when the subscription commenced
6. Subscription End: Date when the subscription ended
7. Cancelled: Shows if the subscription was actually cancelled or not
8. Revenue: Total amount of money made from the packages
9. Subscription Duration: Time the Subscription lasted
    
### TOOLS USED
---
1. Microsoft Excel [Download here](https://www.microsoft.com)
- For Data Input
- For Analysis
- For Data Cleaning
- For Data visualization
  
2. Microsoft SQL Server [Download here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads?msockid=2b7beaf97efb6b170d9dfff87f1b6a9f)
- To manage and querry data
- Microsoft Power BI Download Here
- For Data Transformation
- Data modelling
- To Create reports and dashboards that are collections of visuals.
  
4. GitHub [Click here to sign up](https://github.com/)
- For Portfolio Building

### DATA CLEANING AND PREPARATIONS
---
In the initial phase of the data cleaning and preparations, I perform the following actions;
1. Data loading and inspection; data quality was ensured by correcting any spelling error.
2. Handling missing variables
3. Data cleaning and formatting
4. Data import from Excel to SQL and Power BI

### EXPLORATORY DATA ANALYSIS
---
EDA involved the exploring of the data to answer some questions about the data such as:
This analysis will involve a deep exploration of the data to answer key questions that are essential for effective decision-making. These include:
1. Retrieve the total number of customers from each region.
2. Find the most popular subscription type by the number of customers.
3. Find customers who canceled their subscription within 6 months.
4. Calculate the average subscription duration for all customers.
5. Find customers with subscriptions longer than 12 months.
6. Calculate total revenue by subscription type.
7. Find the top 3 regions by subscription cancellations.
8. Find the total number of active and canceled subscriptions.


### DATA ANALYSIS
---
Here are some lines of code, queries & some of the DAX expressions used during my analysis;

```SQL
SELECT * FROM [dbo].[CUSTOMERDATA]

	---RETRIEVING THE TOTAL NUMBER OF CUSTOMERS FROM EACH REGION---

SELECT  REGION, 
COUNT(DISTINCT CUSTOMERID) AS TOTAL_CUSTOMERS 
FROM [dbo].[CUSTOMERDATA]
GROUP BY REGION;

	---FINDING THE MOST POPULAR SUBSCRIPTION TYPE BY THE NUMBER OF CUSTOMERS---

SELECT TOP 1 SUBSCRIPTIONTYPE, 
COUNT(DISTINCT CUSTOMERID) AS TOTAL_CUSTOMERS
FROM [dbo].[CUSTOMERDATA]
GROUP BY SUBSCRIPTIONTYPE 
ORDER BY TOTAL_CUSTOMERS DESC;

	---FINDING CUSTOMERS WHO CANCELED THEIR SUBSCRIPTION WITHIN 6 MONTHS---

SELECT CUSTOMERID
FROM [dbo].[CUSTOMERDATA]
WHERE 
	DATEDIFF(MONTH, SUBSCRIPTIONSTART, SUBSCRIPTIONEND) <= 6;

	---CALCULATING THE AVERAGE SUBSCRIPTION DURATION FOR ALL CUSTOMERS ---

SELECT AVG(DATEDIFF(DAY, SUBSCRIPTIONSTART, SUBSCRIPTIONEND)) AS AVG_SUBSCRIPTION_DURATION
FROM [dbo].[CUSTOMERDATA]

SELECT 
    AVG(DATEDIFF(MONTH, SUBSCRIPTIONSTART, SUBSCRIPTIONEND)) AS AVERAGE_SUBSCRIPTION_DURATION
FROM 
    [dbo].[CUSTOMERDATA]

	---FINDING CUSTOMERS WITH SUBSCRIPTIONS LONGER THAN 12 MONTHS---

SELECT 
    CUSTOMERID,
    SUBSCRIPTIONSTART,
    SUBSCRIPTIONEND,
    DATEDIFF(MONTH, SUBSCRIPTIONSTART, SUBSCRIPTIONEND) AS SUBSCRIPTION_DURATION
FROM 
    [dbo].[CUSTOMERDATA]
WHERE 
    DATEDIFF(MONTH, SUBSCRIPTIONSTART, SUBSCRIPTIONEND) > 12
ORDER BY 
    SUBSCRIPTION_DURATION DESC;

	---CALCULATING TOTAL REVENUE BY SUBSCRIPTION TYPE---

	SELECT SUBSCRIPTIONTYPE,
SUM(REVENUE) AS TOTAL_REVENUE 
FROM [dbo].[CUSTOMERDATA]
GROUP BY SUBSCRIPTIONTYPE;

---FIND THE TOP 3 REGIONS BY SUBSCRIPTION CANCELLATIONS---
SELECT TOP 3 REGION,
COUNT(*) AS SUBSCRIPTION_CANCELATION_BY_REGION
FROM [dbo].[CUSTOMERDATA]
WHERE CANCELED = 'TRUE'
GROUP BY REGION
ORDER BY SUBSCRIPTION_CANCELATION_BY_REGION DESC;

---FIND THE TOTAL NUMBER OF ACTIVE AND CANCELED SUBSCRIPTION---
SELECT * FROM [dbo].[CUSTOMERDATA]
SELECT 
  COUNT(CASE WHEN Canceled = '1' THEN 1 END) AS TOTAL_ACTIVE,
  COUNT(CASE WHEN Canceled = '0' THEN 0 END) AS TOTAL_CANCELED
FROM 
  [dbo].[CUSTOMERDATA];

``` 

### DATA VISUALIZATION
---
