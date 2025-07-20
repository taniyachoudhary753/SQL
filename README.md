This project is to showcase my SQL Queries related to insight generation based on the acquired results

Query-1

-- Total sales by Product Category

SELECT 
    Product_Category,
    SUM(Amount) AS Total_Sales,
    COUNT(*) AS Total_Orders
FROM
    `project sales`
GROUP BY Product_Category
ORDER BY Total_Sales DESC;

<img width="359" height="161" alt="image" src="https://github.com/user-attachments/assets/2c03e078-5429-43bb-9135-a1199a330ad3" />

Query-2

-- most commonly ordered product category

SELECT 
    Product_Category,
    COUNT(Orders) AS Total_Orders,
    SUM(Orders) AS Total_Quantity,
    SUM(Amount) AS Total_Sales
FROM
    `project sales`
GROUP BY Product_Category
ORDER BY Total_Quantity DESC
LIMIT 1;

<img width="495" height="62" alt="image" src="https://github.com/user-attachments/assets/f10870ac-e2e7-466a-aec1-83232f0db4be" />

Query-3

-- Rank top customers by total spend

SELECT
  Cust_name,
  SUM(Amount) AS Total_Spend,
  RANK() OVER (ORDER BY SUM(Amount) DESC) AS Customer_Rank
FROM `project sales`
GROUP BY Cust_name;

<img width="337" height="242" alt="image" src="https://github.com/user-attachments/assets/0102992a-ec3f-49bb-b77c-a93668fe1155" />

Query-4

-- Orders placed in the first quarter by Southern zone customers

SELECT 
    *
FROM
    `project sales`
WHERE
    Zone = 'Southern'
        AND STR_TO_DATE(Date, '%d-%b-%y') BETWEEN '2025-01-01' AND '2025-03-31';
       
<img width="1265" height="217" alt="image" src="https://github.com/user-attachments/assets/2725a00d-33d5-4861-822c-d998e507265a" />

        Query-5

        -- Customers whose total spend is above average
        
SELECT 
    Cust_name, SUM(Amount) AS Total_Spend
FROM
    `project sales`
GROUP BY Cust_name
HAVING SUM(Amount) > (SELECT 
        AVG(TotalSpend)
    FROM
        (SELECT 
            SUM(Amount) AS TotalSpend
        FROM
            `project sales`
        GROUP BY Cust_name) AS CustomerTotals);

<img width="282" height="250" alt="image" src="https://github.com/user-attachments/assets/d8431d7d-973f-43d8-a77d-a2089ee08ab4" />

Query-6

-- Total sales and orders per month

SELECT 
    DATE_FORMAT(STR_TO_DATE(Date, '%d-%b-%y'), '%Y-%m') AS Month,
    COUNT(*) AS Total_Orders,
    SUM(Amount) AS Total_Sales
FROM
    `project sales`
GROUP BY Month
ORDER BY Month;

<img width="306" height="245" alt="image" src="https://github.com/user-attachments/assets/13eda099-6b51-46d1-afdd-06ee00ba49de" />

Query-7

-- States contributing the most revenue

SELECT 
    State, SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY State
ORDER BY Total_Revenue DESC
LIMIT 5;

<img width="306" height="141" alt="image" src="https://github.com/user-attachments/assets/08d9d58a-7e42-4a97-b819-a7f93340f13c" />

Query-8

-- How much each product category is contributing

SELECT 
    Product_Category,
    SUM(Amount) AS Category_Revenue,
    COUNT(*) AS Total_Orders
FROM `project sales`
GROUP BY Product_Category
ORDER BY Category_Revenue DESC;

<img width="425" height="157" alt="image" src="https://github.com/user-attachments/assets/0b95479f-df70-42c8-81f2-26185d3982da" />













        










