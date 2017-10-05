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


### Weather Observation Station 6- 12 
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
**or**
```
regexp_like(city,'^[aeiou]','i') 
```
in this example the 'i' is the match_parameter 
[regexp_like example](http://ramkedem.com/en/oracle-regexp_like/)

### Weather Observation Station 7
Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

My answer:
```
select distinct city 
from station
where regexp_like (lower(city), '(*)[aeiou]$');
```
or
```
select distinct city 
from station
where regexp_like (lower(city), '[aeiou]$');
```

### Weather Observation Station 8
Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

My answer:
```
select distinct city 
from station
where regexp_like (city, '^[aeiou]','i') and regexp_like(city, '[aeiou]$','i');
```

### Weather Observation Station 9-10
Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.

My answer
```
select distinct city
from station
where not regexp_like(city,'^[aeiou]','i');
```
using "not"

### Weather Observation Station 11-12
Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

My answer:
```
select distinct city
from station
where not regexp_like(city, '^[aeiou]','i') or not regexp_like(city,'[aeiou]$','i');
```


### Higher Than 75 Marks
Query the Name of any student in STUDENTS who scored higher than 75 Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

My answer:
```
select name
from students
where marks > 75
order by substr(name,-3,3) , id asc ;
```
