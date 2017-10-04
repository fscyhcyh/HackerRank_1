# HackerRank_1
SQL

## Basic Select
### Weather Observation Station 4
Let  be the number of CITY entries in STATION, and let  be the number of distinct CITY names in STATION; query the value of  from STATION. In other words, find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

my answer
```
select count(city)- count(distinct city)
from station ;
```

### Weather Observation Station 5
**This is the points that i don't know: row number **
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
Sample Input

Let's say that CITY only has four entries: DEF, ABC, PQRS and WXY
Sample Output
ABC 3
PQRS 4
