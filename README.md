# LITA PROJECT
---------------------------------------------

### Project Title: MY LITA PROJECT DOCUMENTATION
----------------------------------------------------------------

### Project Overview: 
----------------------------------------
This Data Analysis project develops an interactive sales analytics dashboard using Microsoft Excel, SQL, and powerBI. The dashboard provides insights into sales trend, customer behaviour, and product performance, enabling data-driven decisions.

### Technologies Used:
--------------------------------------------------------------------------------------------------------------------------
  - Microsoft Excel(data modeling, data visualisation)
  - SQL (data extraction, querying)
  - PowerBI (data visualisation, reporting)
  - Github (documentation)

  ### Project Information:
----------------------------------------------------------------------------------------------------------------------------------
  This project analysed two datasets using Microsoft Excel, SQL, and POWERBI to answer some key business related questions

  ### Dataset description
  ----------------------------------------------------------------------------------------
# Dataset 1: Capstone Data
    Source: LITA
    Columns/Variables: OrderID, CustomerID, Region, Quantity, Revenue...

# Dataset 2: Customer Data
    Source: LITA
    Columns/Variables: Revenue, Subscription start, Subscription end, Cancelled.
  
## Methodology    
    ---------------------------------------------------------------------------
 + Data Cleaning and Preparation
   
 _**Used Microsoft Excel**_
 
 - removed duplicates first
 - created a revenue column on capstone data
 - performed some metrics using formulas
 - used pivot table to showcase average and sums of some values
 - used pivot table to create charts(bar chart, pie chart and flow chart).

## MICROSOFT EXCEL VISUALIZATION

**FROM CAPSTONE DATASET**

  ![Capstone dataset 2](https://github.com/user-attachments/assets/fffc5ca3-26f3-4c20-a7c9-bba96879ce9e)

   ![Capstone metrics](https://github.com/user-attachments/assets/57485cf8-90d1-4830-8704-19b001e5b722)

![Capstone data charts](https://github.com/user-attachments/assets/dfdbf91a-d7c9-4b97-9ea7-f2bf2c1a02b6)

**FROM CUSTOMER DATA**

![Customer data pivot tables](https://github.com/user-attachments/assets/4816241e-49bb-473a-b0e0-76d7bec89233)

![Customer data pivot tables 2](https://github.com/user-attachments/assets/72ba52e3-0dcf-4232-971e-5b3eaf83a31e)

![Customer data pivot table 3](https://github.com/user-attachments/assets/af32dbb3-126c-4f96-9ff0-62e753884491)

_**USED SQL**_

**QUERIES USED FOR THE CAPSTONE DATASET**
    SELECT * FROM [LITA PROJECT];

--- 1. retrieve the total sales for each product category.---
SELECT Product, SUM(Quantity) AS TotalSales
FROM [LITA PROJECT]
GROUP BY Product

EXEC sp_rename 'LITA PROJECT.TOTAL SALES', 'Quantity', 'COLUMN';


--- 2. find the number of sales transactions in each region.
SELECT Region, COUNT(OrderID) AS NumOfTransactions
FROM [LITA PROJECT]
GROUP BY Region


-- 3. find the highest-selling product by total sales value.--
SELECT Top (1) Product, SUM(Quantity) AS TotalSales
FROM [LITA PROJECT]
GROUP BY Product
ORDER BY TotalSales DESC


--- 4. calculate total revenue per product.---
SELECT Product, SUM(Quantity) AS TotalRevenue
FROM [LITA PROJECT]
GROUP BY Product


-- 5. calculate monthly sales totals for the current year
SELECT Month(OrderDate) AS Month,
    SUM(Quantity) AS MonthlySalesTotal
FROM [LITA PROJECT] WHERE YEAR(OrderDate) = 2024
GROUP BY Month(OrderDate)
ORDER BY Month


-- 6. find the top 5 customers by total purchase amount.---
SELECT Top (5) Customer_Id,
 SUM(Quantity) AS TotalPurchaseAmount FROM [LITA PROJECT]
GROUP BY Customer_Id
ORDER BY TotalPurchaseAmount DESC


-- 7. calculate the percentage of total sales contributed by each region.---
SELECT Region, SUM(Quantity) AS RegionTotalSales,
FORMAT(ROUND((SUM(Quantity) / CAST(SELECT SUM(Quantity) FROM LITA PROJECT) AS DECIMAL(10,2)) * 100), 1), '0.#')
AS PercentageOfTotalSales
FROM * [LITA PROJECT]
GROUP BY Region
ORDER BY PercentageOfTotalSales DESC

-- 8. identify products with no sales in the last quarter.---
SELECT Product FROM [LITA PROJECT]
GROUP BY Product
HAVING SUM(CASE 
WHEN OrderDate BETWEEN '2024-06-01' AND '2024-08-31' 
THEN 1 ELSE 0 END) = 0

    QUERIES USED FOR THE CUSTOMER DATASET

    SELECT * FROM CUSTOMER

-- 1. retrieve the total number of customers from each region.---

SELECT Region, COUNT(CustomerID) AS TotalCustomers
FROM Customer
GROUP BY Region;

-- 2. find the most popular subscription type by the number of customers.--

SELECT SubscriptionType, COUNT(CustomerID) AS MostPopularSubscriptionType
FROM Customer
GROUP BY SubscriptionType
ORDER BY MostPopularSubscriptionType DESC;

SELECT Top (1) SubscriptionType, COUNT(CustomerID) AS MostPopularSubscriptionType
FROM Customer
GROUP BY SubscriptionType
ORDER BY MostPopularSubscriptionType DESC
 


-- 3. find customers who canceled their subscription within 6 months.--

SELECT CustomerName, SubscriptionStart, SubscriptionEnd
FROM Customer
WHERE Canceled = 'TRUE';



-- 4. calculate the average subscription duration for all customers.--

SELECT AVG(DATEDIFF(SubscriptionStart, SubscriptionEnd)) AS AverageSubscriptionDuration
FROM Customer;




-- 5. find customers with subscriptions longer than 12 months.--

SELECT *
FROM Customer
WHERE DATEDIFF(SubscriptionEnd, SubscriptionStart) > 365;


-- 6. calculate total revenue by subscription type.--
SELECT SubscriptionType, SUM(Revenue) AS TotalRevenue
FROM Customer
GROUP BY SubscriptionType
ORDER BY TotalRevenue DESC
 


-- 7. find the top 3 regions by subscription cancellations.

SELECT  Top (3) Region, COUNT(CustomerID) AS Cancellations
FROM Customer WHERE Canceled = 'TRUE'
GROUP BY Region
ORDER BY Cancellations DESC;


-- 8. find the total number of active and canceled subscriptions.
SELECT 
    SUM(CASE WHEN Canceled = 'TRUE' THEN 1 ELSE 0 END) AS TotalCanceled,
    SUM(CASE WHEN Canceled = 'FALSE' THEN 1 ELSE 0 END) AS TotalActive
FROM Customer;

 - created a database, named it LITA PROJECT
 - imported a flat file which is the clean csv format dataset 
 - wrote my queries in line with the project questions asked
 - executed the queries as I wrote them. 

RESULTS SHOWN
![SQL 1](https://github.com/user-attachments/assets/2449612b-a8c9-49d7-b1b9-a1d821f89537)

![SQL 2](https://github.com/user-attachments/assets/56e39b2b-d721-4832-bc37-60ff870f4e07)

![SQL customerdata](https://github.com/user-attachments/assets/1914fd82-2d4d-461e-b3cc-45e2b480d2aa)

### CONCLUSION FROM SQL



    
