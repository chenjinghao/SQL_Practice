# LeetCode SQL 50 Study Plan
[Visit the study plan](https://leetcode.com/studyplan/top-sql-50/)
## Level: Medium
### 180 Consecutive Number
```
SELECT 
	DISTINCT l1.num as ConsecutiveNums 
FROM 
	Logs AS l1 JOIN Logs AS l2 ON l1.id + 1 = l2.id AND l1.num = l2.num
			JOIN Logs AS l3 ON l2.id + 1 = l3.id AND l2.num = l3.num;
```
### 1943 Confirmation Rate
```
WITH CTE AS (
	SELECT
	    user_id,
	    SUM(CASE 
		    WHEN action = 'confirmed' 
		    THEN 1  
		    ELSE 0 
		    END) AS num_cfm,
	    COUNT(user_id) AS requested
	FROM
	    Confirmations
	Group by 
	    user_id)

SELECT 
	s.user_id, 
    	(CASE 
	    WHEN requested IS NULL   
	    THEN 0 
	    ELSE ROUND((num_cfm / requested), 2) 
	    END) AS confirmation_rate
FROM
    Signups AS s LEFT JOIN
    CTE ON s.user_id = cte.user_id
```
### 176 Second Highest Salary
```
WITH CTE AS (SELECT 
                id,
                salary, 
                RANK() OVER(ORDER BY salary DESC) AS ranked
            FROM Employee
            GROUP BY salary)

SELECT 
    MAX(CASE WHEN ranked=2 THEN salary end) AS SecondHighestSalary
FROM
    CTE;
```
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
--Run time: 493ms
--Beats 97.52%
-- @11 July 2025

WITH CTE AS (
    SELECT player_id, event_date,
    RANK() OVER(PARTITION BY player_id ORDER BY event_date) AS rank_year
FROM
    Activity)

SELECT
    ROUND(COUNT(*)/(SELECT COUNT(distinct player_id) FROM Activity),2) AS fraction
FROM CTE AS c1 LEFT JOIN
    CTE AS c2 ON c1.player_id = c2.player_id
WHERE c1.rank_year =1
    AND c2.rank_year =2
    AND date_add(c1.event_date, INTERVAL 1 DAY) = c2.event_date
```
### 1174 Immediate Food Delivery 2
```
--Run time: 545 ms
--Beats 97.95%
-- @11 July 2025
WITH CTE AS (
    SELECT
        customer_id,
        order_date, 
        customer_pref_delivery_date, 
        RANK() OVER(PARTITION BY customer_id ORDER BY order_date) as rank_year
    FROM 
        Delivery)

SELECT 
		ROUND((
			(SELECT COUNT(*)
			FROM cte 
			WHERE rank_year = 1
			    AND order_date = customer_pref_delivery_date) / 
	    (SELECT COUNT(*)
			FROM cte 
			WHERE rank_year = 1) * 100),2) AS immediate_percentage
FROM 
    Delivery
LIMIT 1
```
### 1193 Monthly Transactions 1
```
    SELECT
        SUBSTRING(trans_date,1,7) as month,
        --CONCAT(YEAR(trans_date), '-', LPAD(MONTH(trans_date), 2, '0')) AS month,
        --change to above link can boost up the speed
        country,
        COUNT(*) AS trans_count,
        SUM(CASE 
            WHEN state ="approved" THEN 1 ELSE 0 
        END) as approved_count,
        SUM(amount) as trans_total_amount, 
        SUM(CASE
            WHEN state='approved' THEN amount ELSE 0
        END) AS approved_total_amount
    FROM
        Transactions
    GROUP BY month, country;
```
### 570 Managers with at Least 5 Direct Reports
```
WITH CTE AS (
    SELECT managerId,
        name,
        COUNT(*) as count_report
    FROM Employee
    GROUP BY managerId
    HAVING COUNT(*) >= 5

)
SELECT
    e.name as name
FROM 
    CTE LEFT JOIN
    Employee AS e ON CTE.managerId = e.id
WHERE cte.name IS NOT NULL
    AND CTE.managerId = e.id
    OR e.id IS NOT NULL;
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

### 1757. Recyclable and Low Fat Products
```
# Write your MySQL query statement below
SELECT 
    product_id
FROM 
    Products
WHERE 
    low_fats = 'Y' 
    AND recyclable = 'Y';
```
