## [10] Quiz 2

```
SELECT artist, SUM(streams)
  FROM Songstreams
 WHERE (year=2020) AND (platform='AppleMusic')
 GROUP BY artist
HAVING SUM(streams)>10000000
 ORDER BY SUM(streams) DESC
```

### [10] SELECT & FROM
- [1] `SELECT artist, SUM(streams)`
- [1] `FROM Songstreams`
- [2] `WHERE (year = 2020) AND (platform='AppleMusic')`
- [2] `GROUP BY artist`
- [2] `HAVING SUM(streams)>10000000`
- [2] `ORDER BY SUM(streams) DESC`
