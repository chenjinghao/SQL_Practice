# LeetCode SQL 50 Study Plan
[Visit the study plan](https://leetcode.com/studyplan/top-sql-50/)
## Level: Medium
### 1054 Customers Who Bought All Products
```
SELECT 
    customer_id
FROM 
    Customer
GROUP BY 
    customer_id
HAVING 
    COUNT(DISTINCT product_key) = (SELECT COUNT(DISTINCT product_key) FROM Product)
```

### 1070. Product Sales Analysis III
```
SELECT 
    product_id, 
    year as first_year, 
    quantity, 
    price
FROM 
    Sales
WHERE (product_id, year) IN (
                                SELECT product_id, 
                                    MIN(year) AS first_year
                                FROM 
                                    Sales
                                GROUP BY 
                                    product_id
                            )
```
### 550 Game Play Analysis IV
```
SELECT
	ROUND(COUNT(*)/(SELECT COUNT(distinct player_id) FROM Activity),2) AS fraction
FROM 
	Activity AS a1 LEFT JOIN
	Activity AS a2 ON a1.event_date +1 = a2.event_date
WHERE 
	a1.player_id = a2.player_id
```
### 1174 Immediate Food Delivery 2
```
WITH CTE AS (SELECT customer_id, 
        MIN(order_date) AS first_order_date,
        CASE 
		WHEN MIN(order_date) = customer_pref_delivery_date 
	        THEN 1 ELSE 0 
	END AS immidiate 
FROM Delivery
GROUP BY customer_id)

SELECT ((SUM(immidiate)/COUNT(*))*100) AS immediate_percentage
FROM CTE
```
### 1193 Monthly Transactions 1
```
    SELECT
        SUBSTRING(trans_date,1,7) as month,
        country,
        COUNT(*) AS trans_count,
        CASE 
            WHEN state ="approved" THEN 1 ELSE 0 
        END as approved_count,
        SUM(amount) as trans_total_amount, 
        CASE
            WHEN state='approved' THEN amount ELSE 0
        END AS approved_total_amount
    FROM
        Transactions
    GROUP BY month, country;
```
### 570 Managers with at Least 5 Direct Reports
```
WITH CTE AS (
    SELECT managerId,
        COUNT(*) as count_report
    FROM Employee
    GROUP BY managerId
    HAVING COUNT(*) >= 5
)

SELECT  e.name as name
FROM 
    CTE LEFT JOIN
    Employee as e ON CTE.managerId = e.id
```
## Level: Easy
### 1757. Recyclable and Low-Fat Products
```
SELECT 
	product_id
FROM 
	Products
WHERE
	low_fats = 'Y' 
	and recyclable = 'Y';
```

### 584. Find Customer Referee
```
SELECT
    name
FROM
    Customer
WHERE
    referee_id != 2 
    or referee_id IS NULL;
```

595 Big Countries  
```
SELECT
    name,
    population,
    area
FROM
    World
WHERE
    area >= 3000000
    or population >= 25000000;
```
