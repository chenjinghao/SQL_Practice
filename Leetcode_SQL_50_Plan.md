### 1757. Recyclable and Low-Fat Products
<code>
SELECT 
	product_id
FROM 
	Products
WHERE
	low_fats = 'Y' 
	and recyclable = 'Y';
</code>
