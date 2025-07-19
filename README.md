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
