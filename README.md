This project is to showcase my SQL Queries related to insight generation based on the accuired results

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









