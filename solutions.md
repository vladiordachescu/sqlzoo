# Solutions
## SELECT basics
![world](https://github.com/user-attachments/assets/62b596ad-7c01-4611-a6eb-5060ee894b3a)

1. The example uses a **WHERE** clause to show the population of 'France'. Note that strings should be in 'single quotes';\
   **Modify it to show the population of Germany**
   
```sql
  SELECT population FROM world
  WHERE name = 'Germany';
```
---
2. Checking a list The word **IN** allows us to check if an item is in a list. The example shows the name and population for the countries 'Brazil', 'Russia', 'India' and 'China'.\
   **Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.**

```sql
  SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```
---
3. Which countries are not too small and not too big? **BETWEEN** allows range checking (range specified is inclusive of boundary values). The example below shows countries with an area of 250,000-300,000 sq. km. Modify it to show the country and the area for countries with an area between 200,000 and 250,000.

 ```sql
   SELECT name, area FROM world
   WHERE area BETWEEN 200000 AND 250000;   
 ```
---
## SELECT FROM world

1. [Read the notes about this table](https://sqlzoo.net/wiki/Read_the_notes_about_this_table.). Observe the result of running this SQL command to show the name, continent and population of all countries.
 
 ```sql
   SELECT name, continent, population FROM world;
 ```
---
2. [How to use WHERE to filter records](https://sqlzoo.net/wiki/WHERE_filters). Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

 ```sql
   SELECT name FROM world
   WHERE population >= 200000000;
 ```
---
3. Give the `name` and the **per capita GDP** for those countries with a `population` of at least 200 million.

 ```sql
   SELECT name, gdp/population FROM world
   WHERE population >= 200000000;
 ```
---
4. Show the `name` and `population` in millions for the countries of the `continent` 'South America'. Divide the population by 1000000 to get population in millions.

 ```sql
   SELECT name, population/1000000 FROM world
   WHERE continent = 'South America'; 
 ```
---
5. Show the `name` and `population` for France, Germany, Italy

 ```sql
   SELECT name, population FROM world
   WHERE name IN ('France', 'Germany', 'Italy');
 ```
---
6. Show the countries which have a `name` that includes the word 'United'

 ```sql
   SELECT name FROM world
   WHERE name LIKE 'United%';
 ```
---
7. Two ways to be big: A country is **big** if it has an area of more than 3 million sq km or it has a population of more than 250 million.\

**Show the countries that are big by area or big by population. Show name, population and area.**

 ```sql
   SELECT name, population, area FROM world
   WHERE population > 250000000 OR area > 3000000;
 ```
---
8. **Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.**\

    Australia has a big area but a small population, it should be **included**.\
    Indonesia has a big population but a small area, it should be **included**.\
    China has a big population **and** big area, it should be **excluded**.\
    United Kingdom has a small population and a small area, it should be **excluded**.\

 ```sql
   SELECT name, population, area FROM world
   WHERE area > 3000000 XOR population > 250000000;
 ```
---
9. Show the `name` and `population` in millions and the GDP in billions for the countries of the `continent` 'South America'. Use the [ROUND](https://sqlzoo.net/wiki/ROUND) function to show the values to two decimal places.\
**For Americas show population in millions and GDP in billions both to 2 decimal places.**

 ```sql
   SELECT name, ROUND(population/1000000, 2), ROUND(gdp/1000000000, 2) FROM world
   WHERE continent = 'South America';
 ```
---
10. Show the `name` and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

**Show per-capita GDP for the trillion dollar countries to the nearest $1000.**

 ```sql
   SELECT name, ROUND(gdp/population, -3) FROM world
   WHERE gdp >= 1000000000000;
 ```
---
11. Greece has capital Athens.\
    Each of the strings 'Greece', and 'Athens' has 6 characters.\
    **Show the name and capital where the name and the capital have the same number of characters.**
 
 ```sql
   SELECT name, capital FROM world
   WHERE LENGTH(name)=LENGTH(capital);
 ```
---
12. The capital of Sweden is Stockholm. Both words start with the letter 'S'.\
   **Show the name and the capital where the first letters of each match. Don't include countries where the name       and the capital are the same word.**

 ```sql
   SELECT name, capital FROM world
   WHERE LEFT(name, 1)=LEFT(capital, 1)
   AND name!=capital;
 ```
---
13. **Equatorial Guinea** and **Dominican Republic** have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name.\
    **Find the country that has all the vowels and no spaces in its name.**

 ```sql
   SELECT name FROM world
   WHERE name LIKE '%a%'
     AND name LIKE '%e%'
     AND name LIKE '%i%'
     AND name LIKE '%o%'
     AND name LIKE '%u%'
     AND name NOT LIKE '% %';
 ```
---
## SELECT FROM nobel
![nobel](https://github.com/user-attachments/assets/a5cc2b7f-483f-4044-bfee-673ffd5175e9)

1. Change the query shown so that it displays Nobel prizes for 1950.

```sql
  SELECT yr, subject, winner FROM nobel
  WHERE yr = 1950;
```
---
2. Show who won the 1962 prize for literature.

```sql
  SELECT winner FROM nobel
  WHERE yr = 1962
  AND subject = 'literature';
```
---
3. Show the year and subject that won 'Albert Einstein' his prize.

```sql
  SELECT yr, subject FROM nobel
  WHERE winner = 'Albert Einstein';
```
---
4. Give the name of the 'peace' winners since the year 2000, including 2000.

```sql
  SELECT winner FROM nobel
  WHERE yr >= 2000 AND subject = 'peace';
```
---
5. Show all details (**yr**, **subject**, **winner**) of the literature prize winners for 1980 to 1989 inclusive.

```sql
  SELECT yr, subject, winner FROM nobel
  WHERE subject = 'literature'
  AND yr BETWEEN 1980 AND 1989;
```
---
6. Show all details of the presidential winners:

    - Theodore Roosevelt
    - Thomas Woodrow Wilson
    - Jimmy Carter
    - Barack Obama
  
```sql
  SELECT * FROM nobel
  WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter', 'Barack Obama');
```
---
7. Show the winners with first name John

```sql
  SELECT winner FROM nobel
  WHERE winner LIKE 'John %';
```
---
8. Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.

```sql
  SELECT yr, subject, winner
  FROM nobel
  WHERE subject='physics' AND yr = 1980
  OR subject='chemistry' AND yr = 1984;
```
---
9. Show the year, subject, and name of winners for 1980 excluding chemistry and medicine

```sql
  SELECT yr, subject, winner FROM nobel
  WHERE yr = 1980
  AND subject NOT IN ('chemistry', 'medicine');
```
---

10. Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)

```sql
  SELECT yr, subject, winner FROM nobel
  WHERE subject = 'medicine' AND yr < 1910
  OR subject = 'literature' AND yr >= 2004;
```
---
11. Find all details of the prize won by PETER GRÜNBERG

```sql
  SELECT * FROM nobel
  WHERE winner = 'PETER GRÜNBERG';
```
---

12. Find all details of the prize won by EUGENE O'NEILL

```sql
  SELECT * FROM nobel
  WHERE winner = 'EUGENE O\'NEILL';
```
Alternatively:

```sql
  SELECT * FROM nobel
  WHERE winner = "EUGENE O'NEILL";
```
---

13. Knights in order\

**List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.**

```sql
  SELECT winner, yr, subject FROM nobel
  WHERE winner LIKE 'Sir%'
  ORDER BY yr DESC, winner;
```
---
14. The expression **subject IN ('chemistry','physics')** can be used as a value - it will be 0 or 1.\
   **Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.**

```sql
  SELECT winner, subject FROM nobel
  WHERE yr=1984
  ORDER BY IF(subject IN ('physics','chemistry'), 1, 0), subject,winner;
```
---
## SELECT within SELECT (subqueries)
![subqueries](https://github.com/user-attachments/assets/ddc3adef-7d24-455a-8b66-62664eba6f00)
