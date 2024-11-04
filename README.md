# LITA-Capstone-Projects-2

## Project Overview
This project analyzes a dataset of customer subscriptions to identify key trends in customer segments, subscription duration, revenue, and cancellation patterns. 
Using Excel, SQL, and Power BI, this analysis provides insights into customer behavior 
and helps to identify areas for potential improvements in customer retention, revenue growth, and service offerings. 
The dataset includes customer information, subscription details, revenue, and cancellation statuses.

## Background
This dataset captures customer subscription information for a service provider, 
where each record corresponds to a unique customer and includes the following key fields:
- Customer ID and Name: Unique identifiers and names for each customer.
- Region: The geographical segment (North, South, East, West) of the customer.
- SubscriptionType: Type of subscription purchased by the customer.
- Subscription Dates: Start and end dates of each subscription.
- Canceled: Boolean indicating whether the subscription was canceled.
- Revenue: Revenue generated from each subscription.
- Subscription Duration: Length of the subscription period in days.

# The primary objectives of this analysis are to:
- Understand revenue patterns across customer segments.
- Identify cancellation trends and potential reasons for customer churn.
- Discover popular subscription types and average subscription duration.
- Provide stakeholders with actionable insights to optimize revenue and improve customer retention.

# Excel Analysis
### Purpose
Excel was used as an initial analysis tool to quickly organize, summarize, and 
metrics in the dataset. 
It serves as a flexible platform for data exploration and provides quick insights without requiring complex setup.

### Key Steps
- Analyze customer data using pivot tables to find subscription patterns.
- Calculate the average subscription duration and identify the most popular subscription types.
- [Excel Details](https://github.com/user-attachments/assets/6b758378-75fc-4481-a56d-8fde44cfdea7)
- [Excel Details 2](https://github.com/user-attachments/assets/e01ddca2-5e4b-441c-be97-5ed4f5a225f8)


## Summary
Using Excel, I identified SubscriptionDuration for each, while Pivot tables revealed key customer segments and showed which subscription types are most popular.

# SQL Analysis
### Purpose 
SQL was used to query the data, aggregate results, and conduct deeper analysis. 
SQL queries provide precise and efficient ways to handle large datasets, automate calculations, and enable structured reporting.

### Key SQL Queries
- retrieve the total number of customers from each region.
  - SELECT 
    Region,
    COUNT(CustomerID) AS TotalCustomers
FROM [dbo].[LITA_Capstone_Customerdata]
GROUP BY Region
ORDER BY TotalCustomers DESC;
- [Total Customer](https://github.com/user-attachments/assets/da6fe3c3-13c9-4bb3-86e7-72370ee6b88f)

- find the most popular subscription type by the number of customers.
   -SELECT 
    SubscriptionType,
    COUNT(CustomerID) AS TotalCustomers
FROM [dbo].[LITA_Capstone_Customerdata]
GROUP BY SubscriptionType
ORDER BY TotalCustomers DESC;
- [Most Subscription](https://github.com/user-attachments/assets/ca51e28e-2d2d-4d0b-bb5b-bc7fe6f784ed)

- find customers who canceled their subscription within 6 months.
  - SELECT 
    CustomerID,
    CustomerName,
    Region,
    SubscriptionType,
    SubscriptionStart,
    SubscriptionEnd,
	DATEDIFF(Month, SubscriptionEnd, SubscriptionStart)
FROM [dbo].[LITA_Capstone_Customerdata]
WHERE Canceled = 1
AND DATEDIFF(Month, SubscriptionEnd, SubscriptionStart) <=180;
- [Canceled Subscription within 6month](https://github.com/user-attachments/assets/d2de22d2-c97e-4a6d-8f84-9fca1ec621f9)

- calculate the average subscription duration for all customers.
  - SELECT 
    AVG(DATEDIFF(Month, SubscriptionEnd, SubscriptionStart)) 
	AS AverageSubscriptionDuration
FROM [dbo].[LITA_Capstone_Customerdata];
- [Average Subscription](https://github.com/user-attachments/assets/290495a4-b611-4d93-8c60-8351c960bd1c)

-  find customers with subscriptions longer than 12 months.
  - SELECT 
    CustomerID,
    CustomerName,
    Region,
    SubscriptionType,
    SubscriptionStart,
    SubscriptionEnd,
    Revenue
FROM [dbo].[LITA_Capstone_Customerdata]
WHERE DATEDIFF(Month, SubscriptionEnd, SubscriptionStart) > 365;
- [Subscription longer than 12month](https://github.com/user-attachments/assets/5324b75a-728c-4f7b-bfca-138496275eb3)

- calculate total revenue by subscription type.
  - SELECT 
    SubscriptionType,
    SUM(Revenue) AS TotalRevenue
FROM [dbo].[LITA_Capstone_Customerdata]
GROUP BY SubscriptionType
ORDER BY TotalRevenue DESC;
- [TotalRevenue](https://github.com/user-attachments/assets/a8765dd1-aad0-4d18-8db2-6fc96cf77280)

-  find the top 3 regions by subscription cancellations.
  - SELECT TOP 3
    SubscriptionType,
    COUNT(CustomerID) AS TotalCancellations
FROM [dbo].[LITA_Capstone_Customerdata]
WHERE Canceled = 1
GROUP BY SubscriptionType
ORDER BY TotalCancellations DESC;
- [Top3 Region](https://github.com/user-attachments/assets/f27ca2f2-1d83-47a3-92f8-20401bd17880)

-  find the total number of active and canceled subscriptions
  - SELECT 
    SUM(CASE WHEN Canceled = 1 THEN 1 ELSE 0 END) AS TotalCanceled,
    SUM(CASE WHEN Canceled = 0 THEN 1 ELSE 0 END) AS TotalActive
FROM [dbo].[LITA_Capstone_Customerdata];
- [Total Active and Cancellation](https://github.com/user-attachments/assets/71bd801b-3491-4bfe-a3fe-4a4527f3fa5e)

## Summary
The SQL analysis provided key insights into revenue trends, high-churn regions, and subscription patterns over time. 
SQL allowed us to break down the data at various levels and generate metrics for each region and subscription type. 
The queries also served as a foundation for the Power BI dashboard.

# Power BI Dashboard
## Purpose
Power BI was used to build an interactive dashboard that enables dynamic visualization of customer segments, revenue patterns, 
and subscription trends. 
The dashboard allows stakeholders to explore data visually and filter by different dimensions such as region, subscription type, and customer status.






