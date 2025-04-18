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

#### 595 Big countries
:point_right: https://leetcode.com/problems/big-countries/description/
```
SELECT name, population, area
FROM world
WHERE area >= 3000000 OR population >= 25000000;
```

#### 1148 Article views I
:point_right: https://leetcode.com/problems/article-views-i/description/
```
SELECT DISTINCT ON (author_id) author_id AS id
FROM views
WHERE author_id = viewer_id;
```

#### 1683 Invalid tweets
:point_right: https://leetcode.com/problems/invalid-tweets/description/
```
SELECT tweet_id
FROM tweets
WHERE length(content) > 15;
```

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

#### 1581 Customer who visited but did not make any transactions   
:point_right: https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/  

**LEFT JOIN**, **GROUP BY**, **COUNT**
```
SELECT v.customer_id, COUNT(*) AS count_no_trans
FROM visits v
LEFT JOIN transactions t
ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL 
GROUP BY v.customer_id;
```

#### 197 Rising temperature   
:point_right: https://leetcode.com/problems/rising-temperature/description/

**INNER JOIN**, **INTERVAL**

❗ Data/Time functions and operators in PostgreSQL documentation: https://www.postgresql.org/docs/current/functions-datetime.html

```
SELECT w1.id
FROM weather w1
JOIN weather w2 ON w1.recordDate = w2.recordDate + INTERVAL '1 DAY'
WHERE w1.temperature > w2.temperature;
```

#### 1661 Average time of process per machine   
:point_right: https://leetcode.com/problems/average-time-of-process-per-machine/description/

**INNER JOIN**, **ROUND**, **AVG**, **CAST**, **GROUP BY**

```
SELECT a.machine_id, ROUND(AVG(CAST(b.timestamp - a.timestamp AS DECIMAL)), 3) AS processing_time
FROM activity a
JOIN activity b ON a.machine_id = b.machine_id AND a.process_id = b.process_id AND a.activity_type = 'start' AND b.activity_type = 'end'
GROUP BY a.machine_id;
```

