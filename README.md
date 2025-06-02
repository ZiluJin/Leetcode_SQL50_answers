# Leetcode_SQL50_answers 力扣SQL50道题答案
CONTENT

[Select](#select)

[Basic Joins](#basic-joins)

[Basic Aggregate Functions](#basic-aggregate-functions)
## Select
[1757. Recyclable and Low Fat Products](https://leetcode.com/problems/recyclable-and-low-fat-products/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' and recyclable = 'Y'
```
[584. Find Customer Referee](https://leetcode.com/problems/find-customer-referee/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT name
FROM Customer
WHERE referee_id != '2'
OR referee_id IS NULL
```
[595. Big Countries](https://leetcode.com/problems/big-countries/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000
OR population >=25000000
```
[1148. Article Views I](https://leetcode.com/problems/article-views-i/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY author_id
```
[1683. Invalid Tweets](https://leetcode.com/problems/invalid-tweets/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT tweet_id
FROM Tweets
WHERE length(content)>15
```
## Basic Joins
[1378. Replace Employee ID With The Unique Identifier](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT unique_id, name
FROM Employees
LEFT JOIN EmployeeUNI on Employees.id = EmployeeUNI.id
```
[1068. Product Sales Analysis I](https://leetcode.com/problems/product-sales-analysis-i/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT product_name, year, price
FROM Sales
LEFT JOIN Product on Product.product_id = Sales.product_id
```
[1581. Customer Who Visited but Did Not Make Any Transactions](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT customer_id, COUNT(*) AS count_no_trans
FROM Visits
WHERE visit_id NOT IN (SELECT DISTINCT visit_id FROM Transactions)
 GROUP BY customer_id
```
[197. Rising Temperature](https://leetcode.com/problems/rising-temperature/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON w1.temperature > w2.temperature
AND SUBDATE(w1.recordDate, 1) = w2.recordDate
```
[1661. Average Time of Process per Machine](https://leetcode.com/problems/average-time-of-process-per-machine/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT machine_id, ROUND(AVG(end_time - start_time), 3) as processing_time
FROM(
    SELECT 
        machine_id,
        process_id,
        MAX(CASE WHEN activity_type = 'start' THEN timestamp END) AS start_time,
        MAX(CASE WHEN activity_type = 'end' THEN timestamp END) AS end_time
    FROM Activity
    GROUP BY machine_id, process_id
)t
GROUP BY machine_id;
```
[577. Employee Bonus](https://leetcode.com/problems/employee-bonus/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT name, bonus
FROM Employee e
LEFT JOIN Bonus b
ON e.empId = b.empId
WHERE bonus < 1000 OR bonus IS NULL
```
[1280. Students and Examinations](https://leetcode.com/problems/students-and-examinations/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT stu.student_id, stu.student_name, sub.subject_name, COUNT(exam.subject_name) AS attended_exams
FROM Students stu
CROSS JOIN Subjects sub
    LEFT JOIN Examinations exam
    ON stu.student_id = exam.student_id AND sub.subject_name = exam.subject_name
GROUP BY stu.student_id, sub.subject_name
ORDER BY stu.student_id, sub.subject_name

```
[570. Managers with at Least 5 Direct Reports](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT a.name
FROM Employee a
JOIN(
    SElECT managerId, COUNT(*) AS report_count
    FROM Employee 
    GROUP BY managerId
    HAVING COUNT(*) >= 5
)m
ON a.id = m.managerId
```
[1934. Confirmation Rate](https://leetcode.com/problems/confirmation-rate/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT s.user_id, ROUND(IFNULL(SUM(c.action = 'confirmed') / COUNT(c.action), 0), 2) AS confirmation_rate
FROM
Signups s
LEFT JOIN Confirmations c
ON s.user_id = c.user_id
Group BY s.user_id
```
## Basic Aggregate Functions

[620. Not Boring Movies](https://leetcode.com/problems/not-boring-movies/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT *
FROM cinema
WHERE description != 'boring'
AND mod(id, 2) = 1
ORDER BY rating DESC
```
[1251. Average Selling Price](https://leetcode.com/problems/average-selling-price/description/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT p.product_id, ROUND(IFNULL(SUM(u.units * p.price) / SUM(u.units), 0), 2) AS average_price
FROM Prices p
LEFT JOIN UnitsSold u
ON p.product_id = u.product_id  AND u.purchase_date <= p.end_date AND u.purchase_date >= p.start_date
GROUP BY p.product_id
```
[1075. Project Employees I](https://leetcode.com/problems/project-employees-i/?envType=study-plan-v2&envId=top-sql-50)
```sql
SELECT p.project_id, ROUND(IFNULL(SUM(e.experience_years) / COUNT(p.employee_id), 0), 2) AS average_years
FROM Project p
LEFT JOIN Employee e
ON p.employee_id = e.employee_id
GROUP BY p.project_id
```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
[]()
```sql

```
