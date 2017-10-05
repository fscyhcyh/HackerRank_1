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
**This is the points that i don't know: row number**

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
Sample Input

Let's say that CITY only has four entries: DEF, ABC, PQRS and WXY
Sample Output
ABC 3
PQRS 4

### Weather Observation Station 6
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

The website about [REGEXP_LIKE](https://www.techonthenet.com/oracle/regexp_like.php)
OR 
```
WHERE REGEXP_LIKE (MTD_ITEM_NUMBER,'^(31A-2M5E|31AS2T5F|31A-32AD|31AS62N2|31BM63P3|31AM66Q4|31AH64Q4|31AH55R5|31AM7BR3|31AH54Q6|31AH55Q8)(*)')
```

MY ANSWER
```
select distinct city
from station
where regexp_like(city,'^(a|e|i|o|u|A|E|I|O|U)(*)');
```

To use REGEXP_LIKE is a correct choice! We can also: 
```
regexp_like(lower(city),'^[aeiou](*)') 
```
or
```
regexp_like(lower(city),'^[aeiou]') 
```
