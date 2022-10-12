## [18] Quiz 3
```
SELECT m.title, m.year, count(r.rating), avg(r.rating)
  FROM Movies as m
  JOIN Ratings as r ON m.mid=r.mid
 WHERE m.year > 2000
 GROUP BY m.mid, m.title, m.year
HAVING count(r.rating) >= 1000
 ORDER BY avg DESC
```

- [4] `SELECT m.title, m.year, count(r.rating), avg(r.rating)`
    - [-1] Per column missing
- [4] `FROM Movies as m JOIN Ratings as r ON m.mid=r.mid`
    - [-1] Missing `FROM`
    - [-1] Missing `JOIN Ratings`
    - [-2] Missing `ON m.mid = r.mid`
- [2] `WHERE m.year > 2020`
- [4] `GROUP BY m.mid, m.title, m.year`
    - [-2] Missing m.mid
    - [-1] Missing m.title
    - [-1] Missing m.year
- [2] `HAVING count(r.rating) >= 1000`
- [2] `ORDER BY avg DESC`
