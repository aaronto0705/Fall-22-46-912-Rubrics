## [10] Quiz 1: SQL Basics 

### [7] Question 1:
```
  SELECT Player, Team, Height
    FROM NBAPlayers
   WHERE Height > (SELECT avg(Height) 
                     FROM NBAPlayers)
```
- [+7] Correct
- [2] SELECT
  - [+2] `SELECT Player, Team, Height`
  - [-0.5] Missing one column
  - [-1.5] Missing two columns
- [+1] `FROM NBAPlayers`
- [+1] `WHERE Height >`
- [3] Subquery
  - [+1] `SELECT AVG(height)`
  - [+2] `FROM NBAPlayers`
- [0] Incorrect

### [1] Question 2:
```
  GSW, 198
  LAL, 208
```
- [+1] Correct
- [+0.5] Has `GSW, 198`
- [+0.5] Has `LAL, 208`

### [2] Question 3:
```
  SELECT Team, MAX(Height)
    FROM NBAPlayers
   GROUP BY Team
```
- [+2] Correct
- [+1] `SELECT Team, max(Height) FROM NBAPlayers`
- [+1] `GROUP BY Team`
- [+0] Incorrect
