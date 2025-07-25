" Sales Data Insights & Customer Analytics using SQL "


Project Summary:

“ Developed a comprehensive SQL-based analytics project analyzing transactional sales data for a retail domain. Designed and executed complex queries to generate actionable business insights covering sales trends, customer segmentation, product performance, churn prediction, and regional analysis. Provided clear recommendations to drive sales, optimize inventory, and improve customer retention. ”



Query 1: Total Sales by Product Category

Question: Which product categories generate the highest total sales, and how can we prioritize them to maximize revenue?

Business Goal: Identify top revenue-driving product categories to optimize inventory and marketing efforts.

SELECT 
    Product_Category,
    SUM(Amount) AS Total_Sales,
    COUNT(*) AS Total_Orders
FROM
    `project sales`
GROUP BY Product_Category
ORDER BY Total_Sales DESC;

<img width="359" height="161" alt="image" src="https://github.com/user-attachments/assets/2c03e078-5429-43bb-9135-a1199a330ad3" />

Insight: Footwear & Shoes dominates sales and orders, with Auto and Furniture trailing. Hand & Power Tools underperforms.

Next Step: Prioritize inventory and marketing for Footwear & Shoes, analyze lagging categories for possible improvement or discontinuation.


Query 2: Most Commonly Ordered Product Category

Question: What are the most frequently ordered product categories, indicating strong customer demand?

Business Goal: Understand customer preferences to improve stock availability and drive repeat purchases.

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

Insight: Footwear & Shoes leads in both demand and order frequency, indicating strong and consistent customer interest.

Next Step: Ensure stock availability and explore cross-selling. Use this category's success as a benchmark for others.


Query 3: Rank Top Customers by Total Spend

Question: Who are our highest-spending customers, and how can we enhance their loyalty and lifetime value?

Business Goal: Focus retention and upselling strategies on key customers to increase revenue.

SELECT
  Cust_name,
  SUM(Amount) AS Total_Spend,
  RANK() OVER (ORDER BY SUM(Amount) DESC) AS Customer_Rank
FROM `project sales`
GROUP BY Cust_name;

<img width="337" height="242" alt="image" src="https://github.com/user-attachments/assets/0102992a-ec3f-49bb-b77c-a93668fe1155" />

Insight: Neola is the highest-spending customer by a large margin, followed by Eugene and Ashutosh. Top 10 customers contribute significantly to revenue.

Next Step: Launch loyalty programs or special offers for top customers to increase retention and further boost high-value sales.


Query 4: Orders in First Quarter by Southern Zone Customers

Question: What are the order patterns from Southern zone customers in Q1, and which states and segments should we target?

Business Goal: Implement regional marketing tactics to capitalize on seasonal demand and geographic strengths.

SELECT 
    *
FROM
    `project sales`
WHERE
    Zone = 'Southern'
        AND STR_TO_DATE(Date, '%d-%b-%y') BETWEEN '2025-01-01' AND '2025-03-31';
       
<img width="1265" height="217" alt="image" src="https://github.com/user-attachments/assets/2725a00d-33d5-4861-822c-d998e507265a" />

Insight: Southern zone customers placed multiple orders mostly from Andhra Pradesh and Karnataka in Q1 of 2025, with diverse product and occupation segments.

Next Step: Target Southern region with localized marketing and regional promotions, capitalizing on early-year buying trends.


Query 5: Customers Whose Total Spend Is Above Average

Question: Which customers exceed average spending, and how can we personalize engagement to grow their accounts?

Business Goal: Prioritize high-value customer relationships for tailored marketing and enhanced service.
        
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

Insight: Roughly half the customers exceed average total spend, indicating a strong set of high-value accounts.

Next Step: Focus account management and personalized engagement on these above-average spenders to maximize lifetime value.


Query 6: Total Sales and Orders Per Month

Question: How do sales and order volumes vary month-to-month, and when should we prepare for sales peaks?

Business Goal: Optimize inventory and promotional calendars according to seasonal sales trends.

SELECT 
    DATE_FORMAT(STR_TO_DATE(Date, '%d-%b-%y'), '%Y-%m') AS Month,
    COUNT(*) AS Total_Orders,
    SUM(Amount) AS Total_Sales
FROM
    `project sales`
GROUP BY Month
ORDER BY Month;

<img width="306" height="245" alt="image" src="https://github.com/user-attachments/assets/13eda099-6b51-46d1-afdd-06ee00ba49de" />

Insight: Sales and orders peak in January and remain strong through March, showing a post-New Year sales surge.

Next Step: Prepare inventory and targeted campaigns ahead of Q1, and analyze reasons for any seasonal dips after March for smoother sales across all months.


Query 7: States Contributing the Most Revenue

Question: Which states contribute the most to revenue, and how do we allocate resources regionally?

Business Goal: Focus marketing and operations investments on high-performing states to boost sales.

SELECT 
    State, SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY State
ORDER BY Total_Revenue DESC
LIMIT 5;

<img width="306" height="141" alt="image" src="https://github.com/user-attachments/assets/08d9d58a-7e42-4a97-b819-a7f93340f13c" />

Insight: Delhi and Karnataka lead in revenue, with Delhi significantly ahead. Maharashtra lags among the top five.

Next Step: Direct more promotional efforts in Delhi and Karnataka, and re-evaluate strategies for states with lower revenue.


Query 8: Product Category Contribution

Question: What share of revenue and orders does each product category contribute, and how can we balance our portfolio?

Business Goal: Adjust product mix and marketing focus to maximize profitability.

SELECT 
    Product_Category,
    SUM(Amount) AS Category_Revenue,
    COUNT(*) AS Total_Orders
FROM `project sales`
GROUP BY Product_Category
ORDER BY Category_Revenue DESC;

<img width="425" height="157" alt="image" src="https://github.com/user-attachments/assets/0b95479f-df70-42c8-81f2-26185d3982da" />

Insight: Footwear & Shoes drives the highest revenue and orders. Auto is a distant second.

Next Step: Focus inventory and ads around top-performing categories. Review performance of lower-revenue categories.


Query 9: Age Groups Spending the Most

Question: Which customer age groups drive the highest spending, and how should we tailor marketing?

Business Goal: Target age demographics with relevant offers to enhance conversion rates.

SELECT 
    `Age Group`,
    COUNT(DISTINCT User_ID) AS Unique_Customers,
    SUM(Amount) AS Total_Sales
FROM `project sales`
GROUP BY `Age Group`
ORDER BY Total_Sales DESC;

<img width="351" height="206" alt="image" src="https://github.com/user-attachments/assets/2328f779-868e-492e-ad1a-1d56a6a55ee1" />

Insight: Customers aged 26–35 and 36–45 are the biggest spenders. Younger and older groups contribute less.

Next Step: Tailor marketing campaigns toward the 26–45 age segments to maximize sales impact.


Query 10: Comparing Zones by Revenue

Question: How does revenue and order volume compare across zones, and which underperforming zones need attention?

Business Goal: Expand market penetration and address weaknesses in low-performing regions.

SELECT 
    Zone, COUNT(*) AS Total_Orders, SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY Zone
ORDER BY Total_Revenue DESC;

<img width="339" height="140" alt="image" src="https://github.com/user-attachments/assets/b4287119-2ad6-45dd-908f-7dd30f189201" />

Insight: Central and Southern zones dominate both revenue and order counts. Eastern zone shows minimal activity.

Next Step: Expand successful strategies from Central and Southern zones to weaker zones.Investigate causes for low Eastern zone performance.


Query 11: Calculating Average Order Value (AOV)

Question: What is the average order value, and what strategies can increase it?

Business Goal: Improve profitability by encouraging larger or higher-value transactions.

SELECT 
    SUM(Amount) / SUM(Orders) AS Average_Order_Value
FROM
    `project sales`;

<img width="231" height="70" alt="image" src="https://github.com/user-attachments/assets/615b81e4-21b8-45e0-99ec-8c89f974cea5" />

Insight: The average order value is ₹8,759.66, indicating generally high-value purchases across all transactions.

Next Step: Encourage larger basket sizes through bundling or discount offers, aiming to increase AOV further.


Query 12: Marital Status Impact on Buying

Question: How does marital status influence buying behavior and revenue contribution?

Business Goal: Develop targeted campaigns that resonate with key customer segments.

SELECT 
    Marital_Status,
    COUNT(*) AS Total_Orders,
    SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY Marital_Status;

<img width="399" height="102" alt="image" src="https://github.com/user-attachments/assets/aed10be8-69c4-4647-b770-3fa806447b2f" />

Insight: Singles (Marital_Status=0) place more orders and generate higher revenue than married customers.

Next Step: Target singles with tailored marketing campaigns and promotions to further drive sales.


Query 13: How Many Customers Stick Around (Repeat vs One-Time)

Question: What proportion of customers are repeat buyers versus one-time purchasers, and how can we increase retention?

Business Goal: Grow customer loyalty to boost recurring sales.

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

Insight: Most customers are one-time buyers (253), but repeat customers (19) contribute substantial revenue.

Next Step: Launch retention strategies and loyalty programs to convert more one-time buyers into repeat buyers.


Query 14: Identify Bestseller Products

Question: Which products are bestsellers, and how can we promote them to maximize revenue?

Business Goal: Focus sales and marketing efforts on high-performing products.

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

Insight: Only a few products are ordered frequently (top products have 3 orders each), but with significant revenue.

Next Step: Promote top-performing products more aggressively and analyze why other products aren’t bestsellers.


Query 15: Revenue by Occupation

Question: How does customer occupation impact purchases, and which occupations present growth opportunities?

Business Goal: Target marketing and product offerings to high-value occupational segments.

SELECT 
    Occupation,
    COUNT(*) AS Total_Orders,
    SUM(Amount) AS Total_Revenue
FROM
    `project sales`
GROUP BY Occupation
ORDER BY Total_Revenue DESC;

<img width="416" height="239" alt="image" src="https://github.com/user-attachments/assets/27ac77c4-7f62-4701-9a7a-d84e7bd13ad6" />

Insight: IT Sector and Aviation occupations generate the highest orders and revenue.

Next Step: Focus marketing and partnerships on high-spending occupations to increase market share in these groups.


Query 16: Orders by Gender and Zone

Question: How do order patterns differ by gender across zones, and where should we focus gender-targeted marketing?

Business Goal: Refine campaigns by gender and geography to improve order volumes.

SELECT 
    Gender, Zone, COUNT(*) AS Orders, SUM(Amount) AS Revenue
FROM
    `project sales`
GROUP BY Gender , Zone
ORDER BY Zone , Gender;

<img width="321" height="237" alt="image" src="https://github.com/user-attachments/assets/96886d6c-dbc4-4c05-abec-7d89263bb659" />

Insight: Females in the Central zone drive the highest number of orders and revenue, with the Southern zone also strong.

Next Step: Target Central zone females for campaigns and expand successful tactics to other gender-zone segments.


Query 17: Best Customer by State

Question: Who are the top-spending customers in each state, and how can we recognize and retain them?

Business Goal: Enhance loyalty programs and personalized engagement for key state-level customers.

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

Insight: Each state’s top customer is responsible for the largest spending, with significant revenue concentration.

Next Step: Set up personalized outreach and special rewards for state-level top customers to ensure loyalty.


Query 18: Average Order Value Across Zones

Question: What is the average order value in each zone, and how can zones with lower AOV improve?

Business Goal: Drive higher-value purchases through zone-specific strategies.

SELECT 
    Zone, SUM(Amount) / SUM(Orders) AS Average_Order_Value
FROM
    `project sales`
GROUP BY Zone
ORDER BY Average_Order_Value DESC;

<img width="282" height="139" alt="image" src="https://github.com/user-attachments/assets/a3047150-9b43-4677-bec0-06bf4238aea2" />

Insight: Central zone leads in average order value, followed by Western and Southern. Eastern lags behind.

Next Step: Analyze and replicate high AOV drivers in other zones, especially in low-performance areas like Eastern.


Query 19: Sales Momentum Tracker (Cumulative Sales)

Question: What is the daily sales momentum, and how can we sustain or accelerate it?

Business Goal: Maintain steady growth through timely interventions and campaigns.

SELECT 
    STR_TO_DATE(Date, '%d-%b-%y') AS Sales_Date,
    SUM(Amount) AS Daily_Revenue,
    SUM(SUM(Amount)) OVER (ORDER BY STR_TO_DATE(Date, '%d-%b-%y')) AS Cumulative_Revenue
FROM `project sales`
GROUP BY Sales_Date
ORDER BY Sales_Date;

<img width="399" height="237" alt="image" src="https://github.com/user-attachments/assets/4e93a2a8-7691-4010-ac3e-96f95460c219" />

Insight: Cumulative revenue grows steadily, indicating consistent daily sales momentum in January 2025.

Next Step: Monitor for any dips in momentum and plan campaigns or offers to sustain and boost daily sales.


Query 20: Top Rated Products

Question: Which products have the highest customer ratings, and how can we leverage their reputation?

Business Goal: Use customer satisfaction insights to boost sales and product development.

SELECT 
    ps.product_id, ps.product_Category, pr.rating
FROM
    Product_Rating pr
        JOIN
    `Project Sales` ps ON pr.product_id = ps.product_id
WHERE
    pr.rating = 5;

<img width="364" height="243" alt="image" src="https://github.com/user-attachments/assets/c545dc3f-acad-49fb-986c-d72d74f672a0" />

Insight: Auto category dominates among products rated 5, with Hand & Power Tools only appearing once.

Next Step: Leverage high-rated Auto products in marketing. Investigate how to improve ratings in other categories.


Query 21: Customers at Risk of Churning (Not Ordered in Last 3 Months)

Question: Which customers have not ordered recently and are at risk of churn?

Business Goal: Implement win-back campaigns to reduce customer attrition.

SELECT 
    s.User_ID,
    s.Cust_name,
    MAX(STR_TO_DATE(s.Date, '%d-%b-%y')) AS last_order_date
FROM 
    `project sales` s
GROUP BY 
    s.User_ID, s.Cust_name
HAVING 
    last_order_date IS NULL 
    OR last_order_date < CURDATE() - INTERVAL 3 MONTH;

<img width="350" height="249" alt="image" src="https://github.com/user-attachments/assets/c29d784f-ce35-4d82-ab40-95ca7bdcf775" />

Insight: Several customers haven't placed orders since January 2025, indicating potential churn risk.

Next Step: Initiate win-back campaigns (e.g., emails or special offers) targeting these inactive customers.


Query 22: Customer Segmentation by Age and Gender

Question: How is our customer base distributed by age and gender, and how can segmentation improve marketing effectiveness?

Business Goal: Deliver tailored promotions that resonate with specific segments.

SELECT 
    `Age Group`, 
    Gender, 
    COUNT(DISTINCT User_ID) AS customer_count 
FROM 
    `project sales` 
GROUP BY 
    `Age Group`, Gender;

<img width="308" height="238" alt="image" src="https://github.com/user-attachments/assets/9b5678d2-21fc-4ae0-9db8-8b1845cd2c9a" />

Insight: Age 26–35 males and females are the largest customer segments.

Next Step: Tailor targeted promotions for the 26–35 age group, focusing on both genders for maximum impact.


Query 23: Total Orders and Average Rating per Product

Question: Which products combine high order volume with strong ratings, and which need improvement?

Business Goal: Highlight successful products and address quality issues to enhance sales.

SELECT 
    o.Product_ID,
    COUNT(*) AS order_count,
    ROUND(AVG(r.Rating), 1) AS avg_rating
FROM 
    `project sales` o
JOIN 
    product_rating r ON o.Product_ID = r.Product_ID
GROUP BY 
    o.Product_ID
ORDER BY 
    order_count DESC;

<img width="311" height="238" alt="image" src="https://github.com/user-attachments/assets/ffda4023-2f99-4c86-a492-8be6dfd46c31" />

Insight: Some products (like P00110942) combine high order counts with perfect ratings; others lag behind.

Next Step: Feature best-performing products more prominently. Review and address complaints for lower-rated products.


Query 24: Identifying Duplicate Orders

Question: Are there duplicate orders in the system, and how can we ensure data integrity?

Business Goal: Prevent data errors that could distort reporting and operational decisions.

SELECT 
    User_ID, Product_ID, Date, COUNT(*)
FROM
    `project sales`
GROUP BY User_ID , Product_ID , Date
HAVING COUNT(*) > 1;

<img width="355" height="117" alt="image" src="https://github.com/user-attachments/assets/2a5c25a8-c05a-4ea8-b8bb-c12dcf7a2070" />



Query 25: Locating Null Values

Question: Where are the null or missing values in critical data fields, and how can we improve data quality?

Business Goal: Clean and maintain high-quality data for reliable analytics and decision-making.

SELECT * 
FROM `project sales`
WHERE Date IS NULL OR User_ID IS NULL OR Amount IS NULL;

<img width="1228" height="187" alt="image" src="https://github.com/user-attachments/assets/429fecdc-5420-407c-955b-81dd876ab9e3" />

















































        










