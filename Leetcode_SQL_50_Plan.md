# LeetCode SQL 50 Study Plan
## Level: Medium
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
