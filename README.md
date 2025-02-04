
# Sales Analysis







## Project Overview
The Sales Analysis project is designed to offer valuable insights into a business's sales performance over a specific period. Utilizing SQL, this project showcases common techniques and skills used by data analysts to explore, clean, and analyze retail sales data. It serves as an excellent resource for beginners to understand and apply SQL queries in real-world scenarios.
## Objectives
- **Create a Retail Sales Database**: Set up and populate a retail sales database using the provided sales data.
- **Data Cleaning**: Detect and eliminate records containing missing or null values.
- **Exploratory Data Analysis (EDA)**: Conduct initial exploratory analysis to gain a deeper understanding of the dataset.
- **Business Analysis**: Utilize SQL to address key business questions and extract valuable insights from the sales data.
## Project Structure
 **Database Setup**
Database Creation: The project starts by creating a database named project_1_sales_analysis.
Table Creation: A table named retail_sales is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

**Data Exploration & Cleaning**
Record Count: Determine the total number of records in the dataset.
Customer Count: Find out how many unique customers are in the dataset.
Category Count: Identify all unique product categories in the dataset.
Null Value Check: Check for any null values in the dataset and delete records with missing data.

**Data Analysis & Findings**
The following SQL queries were developed to answer specific business questions:

 Data Analysis and Business key questions and answers


 **Write a SQL query to retrieve all columns for sales made on '2022-11-05:**
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';

**Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022:**

SELECT *
FROM retail_sales
WHERE 
     category = 'Clothing' 
	 AND 
	 TO_CHAR(sale_date,'YYYY-MM') = '2022-11'
	 AND
	 quantiy >= 4;
	 
**Write a SQL query to retrieve all transactions where the category is 'Beauty' and the quantity sold is more than 6 in the month OF Jan-2023:**
SELECT *
FROM retail_sales
WHERE Category = 'Beauty' 
AND
TO_CHAR(sale_date,'YYYY-MM')='2023-01'
AND
quantiy >= 3;
      
	  

**Write a SQL query to calculate the total sales (total_sale) for each category.**
SELECT 
  category,
  sum(total_sale) as net_sale,
  count(*) as total_order
FROM retail_sales
GROUP BY 1;

**Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category**
SELECT 
     ROUND(AVG(age),2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'

**Write a SQL query to find all transactions where the total_sale is greater than 1000.**
 SELECT transactions_id
 FROM retail_sales
 WHERE total_sale > 1000

**Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**
SELECT 
      category,
	  gender,
	  count(*) as total_trans
FROM retail_sales	  	  
GROUP BY
       category,
	   gender

**Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**
SELECT 
      year,
	  month,
	  rank
FROM
(	  
SELECT
	     EXTRACT(YEAR FROM sale_date)as year,
		 EXTRACT(MONTH FROM sale_date)as month,
		 AVG(total_sale) as avg_sale,
		 RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1,2
) as t1
WHERE rank = 1

**Write a SQL query to find the top 5 customers based on the highest total sales **:
SELECT 
      customer_id,
	  SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5

**Write a SQL query to find the top 5 customers based on the lowest total sales **:
SELECT
      customer_id,
	  SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 ASC
LIMIT 5

**Write a SQL query to find the number of unique customers who purchased items from each category.**
SELECT 
      Category,
	  COUNT(DISTINCT(customer_id)) as uni_cs
FROM retail_sales
GROUP BY 1

-- **Write a SQL query to create each shift and number of orders** (Example Morning <12, Afternoon Between 12 & 17, Evening >17)
WITH hourly_sale
AS
(
SELECT *,
      CASE
	      WHEN EXTRACT(HOUR FROM sale_time)<12 THEN 'Morning'
		  WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
		  Else 'Evening'
	  End as shift
FROM retail_sales
)
SELECT 
      shift,
	  COUNT(*) as total_orders
FROM hourly_sale
GROUP BY shift

## Findings
**Customer Demographics:** The dataset covers diverse age groups, with sales spread across categories like Clothing and Beauty.
**High-Value Transactions:** Some transactions exceeded 1000, highlighting premium purchases.
**Sales Trends:** Monthly analysis reveals sales fluctuations, pinpointing peak seasons.
**Customer Insights:** The analysis identifies top-spending customers and the most popular product categories.
## Reports
**Sales Summary**: A comprehensive report covering total sales, customer demographics, and category performance.
**Trend Analysis**: Insights into monthly sales trends and variations.
 **Customer Insights**: Reports highlighting top customers and the unique customer count for each category.
## Conclusion
The analysis provided a comprehensive view of sales performance, offering actionable insights into areas of strength and improvement. By leveraging these insights, businesses can fine-tune their sales strategies, optimize inventory, and improve customer targeting to drive higher revenue growth.


## Professional connect
**LinkedIN** : https://www.linkedin.com/in/sonalika-mishra-472608232/