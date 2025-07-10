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
