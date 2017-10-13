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
**This is the points that i didn't know: analytic functions**

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
Sample Input

Let's say that CITY only has four entries: DEF, ABC, PQRS and WXY
Sample Output
ABC 3
PQRS 4

```
select first_value(city) over (order by len, city), first_value(len) over (order by len, city)
from 
(select city, length(city) len
from station )   
union 
select first_value(city) over (order by len desc, city), first_value(len) over (order by len desc, city)
from 
(select city, length(city) len
from station )  
;
```


### Weather Observation Station 6- 12 
### Weather Observation Station 6
Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

The website about 
[REGEXP_LIKE_2](https://docs.oracle.com/cd/B12037_01/server.101/b10759/conditions018.htm)
[REGEXP_LIKE_2](https://www.techonthenet.com/oracle/regexp_like.php)
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
**Pay attention to order by and [The sequence of the sql clause](http://www.jellythink.com/archives/924)**



## Aggregation
### Average Population 

Query the average population for all cities in CITY, rounded down to the nearest integer.

My Answer:
```
select floor(avg(population))
from city
;
```
**[FLOOR Function (round down)](https://www.techonthenet.com/oracle/functions/floor.php)** 
returns the largest integer value that is equal to or less than a number.

**[Ceil Function (round down)](https://www.techonthenet.com/oracle/functions/ceil.php)** 
returns the smallest integer value that is greater than or equal to a number
 
**[ROUND Function (with numbers)](https://www.techonthenet.com/oracle/functions/round_nbr.php)**
returns a number rounded to a certain number of decimal places


### Population Density Difference  (Basic Select Weather Observation Station 4 --reference)
```
select max(population) - min(population)
from city ; 
```


### The Blunder
Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeroes removed), and the actual average salary.

Write a query calculating the amount of error (i.e.:  average monthly salaries), and round it up to the next integer.
https://www.hackerrank.com/challenges/the-blunder?h_r=next-challenge&h_v=zen

```
select ceil(avg(salary) - avg(to_number(replace(to_char(salary),'0'))))
from employees ;
```

**[Repalce Function](https://www.techonthenet.com/oracle/functions/replace.php)**
**[REGEXP_REPLACE Function 1](https://docs.oracle.com/cd/B19306_01/server.102/b14200/functions130.htm)**
**[REGEXP_REPLACE Function 2](https://www.techonthenet.com/oracle/functions/regexp_replace.php)**

**[Multilingual Regular Expression Syntax](https://docs.oracle.com/cd/B19306_01/server.102/b14200/ap_posix001.htm#i690819)**
**[Regular Expression](https://oracle-base.com/articles/misc/regular-expressions-support-in-oracle#example8)**
