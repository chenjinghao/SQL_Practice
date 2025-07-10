## Level: Medium
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
