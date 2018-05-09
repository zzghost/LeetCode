# Consecutive Numbers
DescriptionHintsSubmissionsDiscussSolution
Write a SQL query to find all numbers that appear at least three times consecutively.
```
+----+-----+
| Id | Num |
+----+-----+
| 1  |  1  |
| 2  |  1  |
| 3  |  1  |
| 4  |  2  |
| 5  |  1  |
| 6  |  2  |
| 7  |  2  |
+----+-----+
```
For example, given the above Logs table, 1 is the only number that appears consecutively for at least three times.
```
+-----------------+
| ConsecutiveNums |
+-----------------+
| 1               |
+-----------------+
```
## Solution
Do self join 2 times.  
```sql
# Write your MySQL query statement below
select T.Num as ConsecutiveNums
from(
select Distinct A.Num from
Logs A
Left join Logs B on A.Id=B.Id-1
Left Join Logs C on A.Id=C.Id-2
Where A.Num = B.Num And A.Num=C.Num
)T
```
