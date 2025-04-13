# [Leetcode 50 SQL questions](https://leetcode.com/studyplan/top-sql-50/)

> :exclamation: All queries are statements for **PostgreSQL** database. 

* [Select](#select)  
* [Basic Joins](#basic-joins)

### Select

#### 1757 Recyclable and low fat products
:point_right: https://leetcode.com/problems/recyclable-and-low-fat-products/description/
```
SELECT product_id 
FROM products
WHERE low_fats = 'Y' AND recyclable = 'Y';
```

#### 584 Find customer referee
:point_right: https://leetcode.com/problems/find-customer-referee/description/
```
SELECT name
FROM customer
WHERE customer.referee_id <> 2;
```
❗ From PostgreSQL documentation:  
<> is the standard SQL notation for “not equal”. != is an alias, which is converted to <> at a very early stage of parsing. Hence, it is not possible to implement != and <> operators that do different things.

### Basic Joins

#### 1378 Replace employee Id with the unique identifier  
:point_right: https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description  

:exclamation: A table order in the FROM clause is important.

* **RIGHT JOIN**  
  ```
  SELECT name, unique_id 
  FROM employeeUNI 
  RIGHT JOIN employees ON employeeUNI.id = employees.id;
  ```
* **LEFT JOIN**
  ```
  SELECT name, unique_id
  FROM employees 
  LEFT JOIN employeeUNI ON employeeUNI.id = employees.id;
  ```

#### 1068 Product sales analisys I  
:point_right: https://leetcode.com/problems/product-sales-analysis-i/description  

**INNER JOIN**
```
SELECT product_name, year, price
FROM Sales
JOIN product ON sales.product_id = product.product_id;
```

