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

Query-9

-- Age groups spending the most

SELECT 
    `Age Group`,
    COUNT(DISTINCT User_ID) AS Unique_Customers,
    SUM(Amount) AS Total_Sales
FROM `project sales`
GROUP BY `Age Group`
ORDER BY Total_Sales DESC;

<img width="351" height="206" alt="image" src="https://github.com/user-attachments/assets/2328f779-868e-492e-ad1a-1d56a6a55ee1" />

Query-10

-- Comparing zones
SELECT 
    Zone, COUNT(*) AS Total_Orders, SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY Zone
ORDER BY Total_Revenue DESC;

<img width="339" height="140" alt="image" src="https://github.com/user-attachments/assets/b4287119-2ad6-45dd-908f-7dd30f189201" />

Query-11

-- Calculating AOV (Average order value)

SELECT 
    SUM(Amount) / SUM(Orders) AS Average_Order_Value
FROM
    `project sales`;

<img width="231" height="70" alt="image" src="https://github.com/user-attachments/assets/615b81e4-21b8-45e0-99ec-8c89f974cea5" />

Query-12

-- Marital status impact on buying (0=Single, 1=Married)

SELECT 
    Marital_Status,
    COUNT(*) AS Total_Orders,
    SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY Marital_Status;

<img width="399" height="102" alt="image" src="https://github.com/user-attachments/assets/aed10be8-69c4-4647-b770-3fa806447b2f" />

Query-13

-- how many customers stick around 

SELECT 
    CASE
        WHEN Order_Count = 1 THEN 'One-time'
        ELSE 'Repeat'
    END AS Customer_Type,
    COUNT(*) AS Num_Customers,
    SUM(Total_Amount) AS Total_Revenue
FROM
    (SELECT 
        User_ID,
            COUNT(*) AS Order_Count,
            SUM(Amount) AS Total_Amount
    FROM
        `project sales`
    GROUP BY User_ID) AS Customer_Orders
GROUP BY Customer_Type;

<img width="435" height="75" alt="image" src="https://github.com/user-attachments/assets/1636d9d9-06c5-4db5-a72a-4c76907c4d17" />

Query-14

-- Identify Bestseller products

SELECT 
    Product_ID,
    COUNT(*) AS Orders_Placed,
    SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY Product_ID
ORDER BY Orders_Placed DESC
LIMIT 10;

<img width="351" height="244" alt="image" src="https://github.com/user-attachments/assets/b5fe9a19-70ca-4e6a-bd21-ed64f70b6857" />

Query-15

-- Revenue by occupation

SELECT 
    Occupation,
    COUNT(*) AS Total_Orders,
    SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY Occupation
ORDER BY Total_Revenue DESC;

<img width="416" height="239" alt="image" src="https://github.com/user-attachments/assets/27ac77c4-7f62-4701-9a7a-d84e7bd13ad6" />

Query-16

-- Orders by Gender and Zone

SELECT 
    Gender, Zone, COUNT(*) AS Orders, SUM(Amount) AS Revenue
FROM
    `project sales`
GROUP BY Gender , Zone
ORDER BY Zone , Gender;

<img width="321" height="237" alt="image" src="https://github.com/user-attachments/assets/96886d6c-dbc4-4c05-abec-7d89263bb659" />

Query-17

-- Best customer by state

WITH State_Customers AS (
    SELECT 
        State,
        Cust_name,
        SUM(Amount) AS Total_Spent,
        ROW_NUMBER() OVER (PARTITION BY State ORDER BY SUM(Amount) DESC) AS rn
    FROM `project sales`
    GROUP BY State, Cust_name
)

SELECT 
    State,
    Cust_name,
    Total_Spent
FROM State_Customers
WHERE rn = 1
ORDER BY State;

<img width="342" height="244" alt="image" src="https://github.com/user-attachments/assets/2cdd4603-658a-448b-996c-54761a94fade" />

Query-18

-- Average order value across zones

SELECT 
    Zone, SUM(Amount) / SUM(Orders) AS Average_Order_Value
FROM
    `project sales`
GROUP BY Zone
ORDER BY Average_Order_Value DESC;

<img width="282" height="139" alt="image" src="https://github.com/user-attachments/assets/a3047150-9b43-4677-bec0-06bf4238aea2" />

Query-19

-- Sales momentum tracker (cumulative sales)

SELECT 
    STR_TO_DATE(Date, '%d-%b-%y') AS Sales_Date,
    SUM(Amount) AS Daily_Revenue,
    SUM(SUM(Amount)) OVER (ORDER BY STR_TO_DATE(Date, '%d-%b-%y')) AS Cumulative_Revenue
FROM `project sales`
GROUP BY Sales_Date
ORDER BY Sales_Date;

<img width="399" height="237" alt="image" src="https://github.com/user-attachments/assets/4e93a2a8-7691-4010-ac3e-96f95460c219" />

Query-20

-- Show top rated products 

SELECT 
    ps.product_id, ps.product_Category, pr.rating
FROM
    Product_Rating pr
        JOIN
    `Project Sales` ps ON pr.product_id = ps.product_id
WHERE
    pr.rating = 5;

<img width="364" height="243" alt="image" src="https://github.com/user-attachments/assets/c545dc3f-acad-49fb-986c-d72d74f672a0" />



































        










