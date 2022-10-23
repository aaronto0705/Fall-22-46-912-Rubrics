## [73] Exam 1 Rubric

### [7] Question 1

```
SELECT customer_id, SUM(quantity*unit_cost)
  FROM Purchases
 WHERE unit_cost >= 1.00
 GROUP BY customer_id
HAVING SUM(quantity*unit_cost) >= 1000
 ORDER BY SUM DESC
 LIMIT 5
```
- [+1] Has `SELECT customer_id, SUM(quantity*unit_cost)` 
- [+1] Has `FROM Purchases`
- [+1] Has `WHERE unit_cost >= 1.00`
- [+1] Has `GROUP BY customer_id`
- [+1] Has `HAVING SUM(quantity*unit_cost) >= 1000`
- [+1] Has `ORDER BY SUM DESC`
- [+1] Has `LIMIT 5`
- [-0.5] Improper use of `HAVING`/`WHERE` (Non-aggregate in `HAVING`, vice-versa)

### [12] Question 2a
```
SELECT s1.name, s2.name, t.cid
  FROM Students as s1
       JOIN Students as s2 on s1.sid < s2.sid
       JOIN Takes as t1 on (t1.sid = s1.sid) 
       JOIN Takes as t2 on (t2.sid = s2.sid)
 WHERE t1.cid = t2.cid
```
- [+3] Has `SELECT s1.name, s2.name, t.cid`
- [+1] Has `FROM` (Students or Takes)
- [+2] Has `s1.sid = s2.sid` check
- [+2] Has `t1.sid = s1.sid` check
- [+2] Has `t2.sid = t2.sid` check
- [+2] Has `t1.cid = t2.cid` check
- [-0] Checks can take place in `WHERE` or `JOIN`
- [-0.5] Improper use of `HAVING`/`WHERE` (Non-aggregate in `HAVING`, vice-versa)

### [7] Question 2b
```
CREATE TABLE Course_Counts AS
    SELECT c.cid, COUNT(t.sid)
      FROM Courses as c
           JOIN Takes as t on c.cid = t.cid
     GROUP BY c.cid
```
- [+2] Has `SELECT c.cid, COUNT(t.sid)`
- [+1] Has `FROM` (Course or Takes) 
- [+2] Joins Courses & Takes together on c.cid = t.cid
- [+2] Has `GROUP BY c.cid`

### [13] Question 2c
```
SELECT c.cid, c.name, COUNT(t.sid)
  FROM Courses as c
       JOIN Takes as t on c.cid = t.cid
 GROUP BY c.cid, c.name
HAVING COUNT(t.sid) = (SELECT MAX(count) FROM Course_Counts)
```

- [+3] Has `SELECT c.cid, c.name, COUNT(t.sid)`
- [+1] Has `FROM` (Course or Takes)
- [+2] Joins Courses & Takes together on c.cid = t.cid
- [+1] Groups by c.cid
- [+2] Groups by c.name
- [+2] Has `HAVING COUNT(t.sid) = ...`
- [+2] Has Subquery: `(SELECT max(count) FROM Course_Counts)`
- [-1] Puts `HAVING` check under `WHERE`

### [4] Question 3a
```
CREATE TABLE Highest_Earnings as 
    SELECT a.year, MAX(a.earnings)
      FROM Athletes as a
     GROUP BY a.year
```

- [+2] Has `SELECT a.year, MAX(a.earnings)`
- [+2] Has `GROUP BY a.year`

### [14] Question 3b
```
SELECT a.name, COUNT(a.year)
  FROM Athletes as a
       JOIN Highest_Earnings  as h
         ON (a.year = h.year) AND 
            (a.earnings = h.max)
 GROUP BY a.name
HAVING COUNT(a.year) > 1
 ORDER BY COUNT DESC, name ASC
```
- [+2] Has `SELECT a.name, COUNT(a.year)`
- [+1] Has `FROM` (Athletes or Highest_Earnings)
- [+1] Joins other Table (Highest_Earnings or Athletes)
- [+2] Checks for (a.year = h.year)
- [+2] Checks for a.earnings = h.max
- [+2] `GROUP BY a.name`
- [+2] Has `HAVING COUNT(a.year) > 1`
- [+1] Orders by COUNT DESC
- [+1] Orders by Name ASC
- [-0] Checks can take place in `WHERE` or `JOIN`
- [-0] Does not specifically state ASC for Name
- [-1] Puts `HAVING` check under `WHERE`

### [16] Question 4
```
SELECT r1.restaurant_id, COUNT(r1.patron_id)
  FROM Ratings as r1
 WHERE r1.rating = 'Excellent'
 GROUP BY restaurant_id
HAVING COUNT(r1.rating) = (SELECT COUNT(r2.rating)
                             FROM Restaurants as r2
                            WHERE r2.restaurant_id = r1.restaurant_id)
```
- [+1] Selects r1.restaurant_id
- [+2] Selects COUNT(r1.patron_id)
- [+1] Has `FROM Rating as r1`
- [+2] Has `WHERE r1.rating = 'Excellent'`
- [+3] Has `GROUP BY restaurant_id`
- [+2] Has `HAVING COUNT(r1.rating) = ...`
- [+5] Subquery
    - [+2] Has `SELECT COUNT(r2.rating)`
    - [+1] Has `FROM Restaurants as r2`
    - [+2] Has `WHERE r2.restaurant_id = r1.restaurant_id`
- [-0.5] Per occurance of improper use of `WHERE`/`HAVING` (Non-aggregates in `HAVING`, vice-versa)
