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
&nbsp;
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
    United Kingdom has a small population and a small area, it should be **excluded**.

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
&nbsp;
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
&nbsp;
## SELECT within SELECT (subqueries)
![subqueries](https://github.com/user-attachments/assets/ddc3adef-7d24-455a-8b66-62664eba6f00)

1. List each country name where the population is larger than that of 'Russia'.

```sql
  SELECT name FROM world
  WHERE population > (SELECT population FROM world
                    WHERE name='Russia');
```
---
2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

```sql
  SELECT name FROM world
  WHERE continent='Europe'
  AND gdp/population > (SELECT gdp/population FROM world
                        WHERE name='United Kingdom');
```
---
3. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

```sql
  SELECT name, continent FROM world
  WHERE continent IN (SELECT continent FROM world
                     WHERE name IN ('Argentina', 'Australia'))
  ORDER BY name;
```

4. Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.

```sql
  SELECT name, population FROM world
  WHERE population > (SELECT population FROM world
  WHERE name='United Kingdom') AND population < (SELECT population FROM world WHERE name = 'Germany');
```
---

5. Germany (population 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany.\
**Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.**

```sql
  SELECT name, CONCAT(ROUND(100*population/(SELECT population FROM world WHERE name='Germany')), "%") AS       
  percentage FROM world 
  WHERE continent='Europe';
```
---

6. Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)

```sql
  SELECT name FROM world
  WHERE gdp > (SELECT MAX(gdp) FROM world
               WHERE continent='Europe');
```
---
7. Find the largest country (by area) in each continent, show the continent, the name and the area:\
   **The above example is known as a correlated or synchronized sub-query.**

```sql
  SELECT continent, name, area FROM world x
  WHERE area >= ALL (SELECT area FROM world y
                   WHERE y.continent=x.continent
                   AND population>0)
```
---
8. List each continent and the name of the country that comes first alphabetically.

```sql
  SELECT continent, name FROM world x
  WHERE name IN (SELECT MIN(name) FROM world y
                 WHERE y.continent=x.continent);
```
---
9. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population. 

```sql
  SELECT name, continent, population FROM world x
  WHERE 25000000 >= (SELECT MAX(population) FROM world y
                   WHERE x.continent=y.continent);
```
---
10. Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.

```sql
  SELECT name, continent FROM world x
  WHERE population > 3*(SELECT MAX(population) FROM world y
  WHERE y.continent=x.continent AND y.name != x.name);
```
---
&nbsp;
## SUM and COUNT

1. Show the total `population` of the world.

```sql
  SELECT SUM(population)FROM world;
```
---
2. List all the continents - just once each.

```sql
  SELECT DISTINCT continent FROM world;
```
---
3. Give the total GDP of Africa

```sql
  SELECT SUM(gdp) FROM world
  WHERE continent = 'Africa';
```
---
4. How many countries have an `area` of at least 1000000

```sql
  SELECT COUNT(*) FROM world
  WHERE area >= 1000000;
```
---
5. What is the total `population` of ('Estonia', 'Latvia', 'Lithuania')

```sql
  SELECT SUM(population) FROM world
  WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```
---
6. For each `continent` show the `continent` and number of countries.

```sql
  SELECT continent, COUNT(*) AS number_of_countries FROM world
  GROUP BY continent;
```
---
7. For each `continent` show the `continent` and number of countries with populations of at least 10 million.

```sql
  SELECT continent, COUNT(*) AS nb_cnt FROM world
  WHERE population >= 10000000
  GROUP BY continent;
```
---
8. List the continents that **have** a total population of at least 100 million. 

```sql
  SELECT continent FROM world
  GROUP BY continent
  HAVING SUM(population)>=100000000;
```
---
&nbsp;
## Join
![games](https://github.com/user-attachments/assets/aa6748ae-6816-42a3-8d87-ae0d34ee1024)
![game tables](https://github.com/user-attachments/assets/3bfcd45c-d3a9-41e3-9be2-a208d1545e2c)

1. The first example shows the goal scored by a player with the last name 'Bender'. The `*` says to list all the columns in the table - a shorter way of saying `matchid`, `teamid`, `player`, `gtime`\
**Modify it to show the <em>matchid</em> and <em>player</em> name for all goals scored by Germany. To identify German players, check for: `teamid = 'GER'`**

```sql
  SELECT matchid, player FROM goal 
  WHERE teamid='GER';
```
---
2. From the previous query you can see that Lars Bender's scored a goal in game 1012. Now we want to know what teams were playing in that match.\
Notice in the that the column `matchid` in the `goal` table corresponds to the `id` column in the `game` table. We can look up information about game 1012 by finding that row in the **game** table.\
**Show id, stadium, team1, team2 for just game 1012**

```sql
  SELECT id,stadium,team1,team2 FROM game
  WHERE id=1012;
```
---
3. You can combine the two steps into a single query with a `JOIN`.
```sql
  SELECT *
  FROM game JOIN goal ON (id=matchid)
```
The **FROM** clause says to merge data from the goal table with that from the game table. The **ON** says how to figure out which rows in **game** go with which rows in **goal** - the **matchid** from **goal** must match **id** from **game**. (If we wanted to be more clear/specific we could say
`ON (game.id=goal.matchid)`\
The code below shows the player (from the goal) and stadium name (from the game table) for every goal scored.\
**Modify it to show the player, teamid, stadium and mdate for every German goal.**

```sql
  SELECT player,teamid,stadium,mdate
  FROM game JOIN goal ON id=matchid
  WHERE teamid='GER';
```
---
4. Use the same `JOIN` as in the previous question.\
**Show the team1, team2 and player for every goal scored by a player called Mario `player LIKE 'Mario%'`**

```sql
  SELECT team1, team2, player
  FROM game
  JOIN goal ON matchid=id
  WHERE player LIKE 'Mario%'
```
---
5. The table eteam gives details of every national team including the coach. You can `JOIN` `goal` to `eteam` using the phrase `goal JOIN eteam on teamid=id`\
**Show `player, teamid, coach, gtime` for all goals scored in the first 10 minutes `gtime<=10`**

```sql
  SELECT player, teamid, coach, gtime
  FROM goal
  JOIN eteam ON teamid=eteam.id
  WHERE gtime <= 10;
```
---
6. To `JOIN` `game` with `eteam` you could use either `game JOIN eteam ON (team1=eteam.id)` or `game JOIN eteam ON (team2=eteam.id)`\
Notice that because `id` is a column name in both `game` and `eteam` you must specify `eteam.id` instead of just `id`\
**List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.**

```sql
  SELECT mdate, teamname
  FROM game
  JOIN eteam ON team1=eteam.id
  WHERE coach='Fernando Santos';
```
---
7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'

```sql
  SELECT player FROM goal
  JOIN game ON matchid=game.id
  WHERE stadium='National Stadium, Warsaw';
```
---
8. The example query shows all goals scored in the Germany-Greece quarterfinal.\
  **Instead show the name of all players who scored a goal against Germany.**

```sql
  SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id
  WHERE (team1= 'GER' OR team2='GER')
  AND teamid != 'GER';
```
---
9. Show teamname and the total number of goals scored.

```sql
  SELECT teamname, COUNT(*)
  FROM eteam JOIN goal ON id=teamid
  GROUP BY teamname;
```
---
10. Show the stadium and the number of goals scored in each stadium.

```sql
  SELECT stadium, COUNT(*) `nmb of goals` FROM game
  JOIN goal ON matchid=game.id
  GROUP BY stadium
```
---
11. For every match involving 'POL', show the matchid, date and the number of goals scored.

```sql
  SELECT matchid,mdate, COUNT(*)
  FROM game JOIN goal ON matchid = id 
  WHERE (team1 = 'POL' OR team2 = 'POL')
  GROUP BY matchid;
```
---
12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'

```sql
  SELECT matchid, mdate, COUNT(*) FROM game
  JOIN goal ON matchid=game.id
  WHERE teamid = 'GER'
  GROUP BY id;
```
---
13. List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises. Sort your result by mdate, matchid, team1 and team2.

```sql
  SELECT mdate,team1,
  SUM(IF(teamid=team1, 1, 0)) AS score1,
  team2,
  SUM(IF(teamid=team2, 1, 0)) AS score2
  FROM game LEFT JOIN goal ON matchid = game.id
  GROUP BY id, mdate, team1, team2
  ORDER BY mdate, matchid, team1, team2;
```
---
&nbsp;
## More JOIN operations
![movies](https://github.com/user-attachments/assets/e33183ac-caaa-4995-844c-ab2a9c49c41e)

1. List the films where the `yr` is 1962 [Show `id, title`]

```sql
  SELECT id, title
  FROM movie
  WHERE yr=1962;
```
---
2. Give year of 'Citizen Kane'.

```sql
  SELECT yr FROM movie
  WHERE title='Citizen Kane';
```
---
3. List all of the Star Trek movies, include the `id`, `title` and `yr` (all of these movies include the words Star Trek in the title). Order results by year.

```sql
  SELECT id, title, yr FROM movie
  WHERE title LIKE '%Star Trek%'
  ORDER BY yr;
```
---
4. What `id` number does the actor 'Glenn Close' have?

```sql
  SELECT id FROM actor
  WHERE name='Glenn Close';
```
---
5. What is the `id` of the film 'Casablanca'

```sql
  SELECT id FROM movie
  WHERE title='Casablanca';
```
---
6. Obtain the cast list for 'Casablanca'.

```sql
  SELECT name FROM actor
  JOIN casting ON actor.id=actorid
  WHERE movieid = (SELECT id FROM movie WHERE title='Casablanca');
```
---
7. Obtain the cast list for the film 'Alien'

```sql
  SELECT name FROM actor
  JOIN casting ON actorid=actor.id
  WHERE movieid = (SELECT id FROM movie WHERE title='Alien');
```
---
8. List the films in which 'Harrison Ford' has appeared

```sql
  SELECT title FROM movie
  JOIN casting ON movie.id=movieid
  WHERE actorid = (SELECT id FROM actor WHERE name='Harrison Ford');
```
---
9. List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the **ord** field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]

```sql
  SELECT title FROM movie
  JOIN casting ON movieid=movie.id
  WHERE actorid = (SELECT id FROM actor WHERE name='Harrison Ford')
  AND ord > 1;
```
---
10. List the films together with the leading star for all 1962 films.

```sql
  SELECT title, name FROM movie
  JOIN casting ON movie.id=movieid
  JOIN actor ON actor.id=actorid
  WHERE yr = 1962 AND ord = 1;
```
---
11. Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

```sql
  SELECT yr,COUNT(title) FROM movie
  JOIN casting ON movie.id=movieid
  JOIN actor ON actorid=actor.id
  WHERE name='Rock Hudson'
  GROUP BY yr
  HAVING COUNT(title) > 2;
```
---
12. List the film title and the leading actor for all of the films 'Julie Andrews' played in.

```sql
  SELECT title, name FROM movie
  JOIN casting ON movie.id=movieid
  JOIN actor ON actor.id=actorid
  WHERE ord = 1 AND movie.id IN (
    SELECT movie.id FROM movie
    JOIN casting ON movieid=movie.id
    WHERE actorid = (SELECT id FROM actor WHERE name = 'Julie Andrews'))
```
---
13. Obtain a list, in alphabetical order, of actors who've had at least 15 starring roles.

```sql
  SELECT name FROM actor
  JOIN casting ON actorid=actor.id
  WHERE ord=1
  GROUP BY name
  HAVING COUNT(*)>=15
  ORDER BY name;
```
---
14.  List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

```sql
  SELECT title, COUNT(actorid) FROM movie
  JOIN casting on movie.id=movieid
  JOIN actor on actor.id=actorid
  WHERE yr=1978
  GROUP BY title
  ORDER BY COUNT(name) DESC, title;
```
---
15. List all the people who have worked with 'Art Garfunkel'.

```sql
  SELECT DISTINCT name FROM casting
  JOIN actor ON actorid = actor.id
  WHERE movieid IN (SELECT movieid FROM movie
		    JOIN casting ON movieid = movie.id
                    JOIN actor ON actorid = actor.id
                    WHERE actor.name = 'Art Garfunkel')
  AND name != 'Art Garfunkel';
```
---
&nbsp;
## Using NULL
![teachers](https://github.com/user-attachments/assets/3a954fdb-c43e-4711-acbc-dd693f1e2b40)

1. List the teachers who have NULL for their department.

```sql
  SELECT name FROM teacher
  WHERE dept IS NULL;
```
---
2. Note the INNER JOIN misses the teachers with no department and the departments with no teacher.

```sql
  SELECT teacher.name, dept.name FROM teacher
  INNER JOIN dept ON (teacher.dept=dept.id);
```
---
3. Use a different JOIN so that all teachers are listed.

```sql
  SELECT teacher.name, dept.name FROM teacher
  LEFT JOIN dept ON teacher.dept=dept.id; 
```
---
4. Use a different JOIN so that all departments are listed.

```sql
  SELECT teacher.name, dept.name FROM teacher
  RIGHT JOIN dept ON teacher.dept = dept.id;
```
---
5. Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no number given. Show teacher name and mobile number or '07986 444 2266'.\
Using the [COALESCE](https://sqlzoo.net/wiki/COALESCE) function

```sql
  SELECT name, COALESCE(mobile, '07986 444 2266') FROM teacher;
```
---
6. Use the COALESCE function and a LEFT JOIN to print the teacher **name** and department name. Use the string 'None' where there is no department.

```sql
  SELECT teacher.name, COALESCE(dept.name, 'None') FROM teacher
  LEFT JOIN dept ON teacher.dept=dept.id;
```
---
7. Use COUNT to show the number of teachers and the number of mobile phones.

```sql
  SELECT COUNT(name), COUNT(mobile) FROM teacher;
```
---
8. Use COUNT and GROUP BY **dept.name** to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.

```sql
  SELECT dept.name, COUNT(teacher.name) FROM teacher
  RIGHT JOIN dept ON teacher.dept=dept.id
  GROUP BY dept.name;
```
---
9. Use CASE to show the **name** of each teacher followed by 'Sci' if the teacher is in **dept** 1 or 2 and 'Art' otherwise.

```sql
  SELECT name, IF(teacher.dept IN (1,2), 'Sci', 'Art') dept FROM teacher;
```
---
10. Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.

```sql
  SELECT name,
  CASE WHEN teacher.dept IN (1,2) THEN 'Sci'
       WHEN teacher.dept = 3 THEN 'Art'
       ELSE 'None'
       END
  FROM teacher;
```
---
&nbsp;
## SELF JOIN
Details of the database Looking at the data

`stops(id, name)`\
`route(num, company, pos, stop)`

1. How many stops are in the database.

```sql
  SELECT COUNT(*) FROM stops;
```
---
2. Find the id value for the stop 'Craiglockhart' 

```sql
  SELECT id FROM stops
  WHERE name='Craiglockhart';
```
---
3. Give the **id** and the **name** for the **stops** on the '4' 'LRT' service.

```sql
  SELECT id, name FROM stops
  JOIN route on id=route.stop
  WHERE company='LRT' AND num='4';
```
---
4. The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

```sql
  SELECT company, num, COUNT(*)
  FROM route WHERE stop=149 OR stop=53
  GROUP BY company, num
  HAVING COUNT(*) = 2;
```
---
5. Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

```sql
  SELECT a.company, a.num, a.stop, b.stop
  FROM route a JOIN route b ON a.company=b.company AND a.num=b.num
  WHERE a.stop=53 AND b.stop = (SELECT id FROM stops WHERE name = 'London Road');
```
---
6. The query shown is similar to the previous one, however by joining two copies of the **stops** table we can refer to **stops** by **name** rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'

```sql
  SELECT a.company, a.num, stopa.name, stopb.name
  FROM route a JOIN route b ON a.company=b.company AND a.num=b.num
    JOIN stops stopa ON a.stop=stopa.id
    JOIN stops stopb ON b.stop=stopb.id
  WHERE stopa.name='Craiglockhart' and stopb.name = 'London Road';
```
---
7. Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith') 

```sql
  SELECT DISTINCT a.company, a.num
  FROM route a JOIN route b ON a.company=b.company AND a.num=b.num
  WHERE a.stop=115 AND b.stop = 137;
```
---
8. Give a list of the services which connect the **stops** 'Craiglockhart' and 'Tollcross'

```sql
  SELECT a.company, a.num
  FROM route a JOIN route b ON a.company=b.company AND a.num=b.num
  JOIN stops stopa ON a.stop=stopa.id
  JOIN stops stopb ON b.stop=stopb.id
  WHERE stopa.name='Craiglockhart' and stopb.name = 'Tollcross'; 
```
---
9. Give a distinct list of the **stops** which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

```sql
  SELECT DISTINCT name, a.company, a.num
  FROM route a
  JOIN route b ON a.company = b.company AND a.num = b.num
  JOIN stops ON a.stop = stops.id
  WHERE b.stop = (SELECT id FROM stops WHERE name='Craiglockhart')
  AND a.company='LRT';
```
---
&nbsp;
## Window functions
![elections](https://github.com/user-attachments/assets/f7c0cf29-3e01-42aa-a1d7-f6e46bf343ea)

1.  Show the `lastName`, `party` and `votes` for the `constituency` 'S14000024' in 2017. 

```sql
  SELECT lastName, party, votes
  FROM ge
  WHERE constituency = 'S14000024' AND yr = 2017
  ORDER BY votes DESC;
```
---
2. You can use the RANK function to see the order of the candidates. If you RANK using (ORDER BY votes DESC) then the candidate with the most votes has rank 1.\
**Show the party and RANK for constituency S14000024 in 2017. List the output by party**

```sql
  SELECT party, votes,
       RANK() OVER (ORDER BY votes DESC) as posn
  FROM ge
  WHERE constituency = 'S14000024' AND yr = 2017
  ORDER BY party;
```
---
3. The 2015 election is a different PARTITION to the 2017 election. We only care about the order of votes for each year.\
**Use PARTITION to show the ranking of each party in S14000021 in each year. Include yr, party, votes and ranking (the party with the most votes is 1).**

```sql
  SELECT yr,party, votes,
      RANK() OVER (PARTITION BY yr ORDER BY votes DESC) as posn
  FROM ge
  WHERE constituency = 'S14000021'
  ORDER BY party,yr;
```
---
4. Edinburgh constituencies are numbered S14000021 to S14000026.\
**Use PARTITION BY constituency to show the ranking of each party in Edinburgh in 2017. Order your results so the winners are shown first, then ordered by constituency.**

```sql
  SELECT constituency,party, votes, RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) posn
  FROM ge
  WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
  AND yr  = 2017
  ORDER BY posn, constituency;
```
---
5. You can use SELECT within SELECT to pick out only the winners in Edinburgh.\
**Show the parties that won for each Edinburgh constituency in 2017.**

```sql
  WITH tb AS (SELECT constituency, party, votes, 
              RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) rnk
              FROM ge
              WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
              AND yr = 2017
              ORDER BY constituency, votes DESC)
  SELECT tb.constituency, tb.party FROM tb
  WHERE tb.rnk = 1;
```
---
6. You can use **COUNT** and **GROUP** **BY** to see how each party did in Scotland. Scottish constituencies start with 'S'\
**Show how many seats for each party in Scotland in 2017.**

```sql
  SELECT party, COUNT(*) 
  FROM (SELECT constituency, party FROM (SELECT constituency, party, votes,
                                         RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS rnk
                                         FROM ge
                                         WHERE constituency LIKE 'S%'
                                         AND yr=2017
                                         ORDER BY rnk, constituency
                                         ) x
         WHERE x.rnk=1) y
  GROUP BY party;
```
---
## COVID 19 (Window LAG)

1. The example uses a WHERE clause to show the cases in 'Italy' in March 2020.\
**Modify the query to show data from Spain**

```sql
  SELECT name, DAY(whn),
   confirmed, deaths, recovered
   FROM covid
  WHERE name = 'Spain'
  AND MONTH(whn) = 3 AND YEAR(whn) = 2020
  ORDER BY whn;
```
---
2. The **LAG** function is used to show data from the preceding row or the table. When lining up rows the data is partitioned by country name and ordered by the data **whn**. That means that only data from Italy is considered.\
**Modify the query to show confirmed for the day before.**

```sql
  SELECT name, DAY(whn), confirmed,
   LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) dbf
  FROM covid
  WHERE name = 'Italy'
  AND MONTH(whn) = 3 AND YEAR(whn) = 2020
  ORDER BY whn;
```
---
3. The number of confirmed case is _cumulative_ - but we can use LAG to recover the number of new cases reported for each day.\**
Show the number of new cases for each day, for Italy, for March.**

```sql
  SELECT name, DAY(whn),
   confirmed-(LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn)) AS new
  FROM covid
  WHERE name = 'Italy'
  AND MONTH(whn) = 3 AND YEAR(whn) = 2020
  ORDER BY whn;
```
---
4. The data gathered are necessarily estimates and are inaccurate. However by taking a longer time span we can mitigate some of the effects.\
You can filter the data to view only Monday's figures **WHERE WEEKDAY(whn) = 0.**\
**Show the number of new cases in Italy for each week in 2020 - show Monday only.**

```sql
  SELECT name, DATE_FORMAT(whn,'%Y-%m-%d'),
         confirmed-(LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn)) AS `new this week`
  FROM covid
  WHERE name = 'Italy'
  AND WEEKDAY(whn) = 0 AND YEAR(whn) = 2020
  ORDER BY whn;
```
---
5. You can JOIN a table using DATE arithmetic. This will give different results if data is missing.\
**Show the number of new cases in Italy for each week - show Monday only.**\
In the sample query we JOIN this week **tw** with last week **lw** using the DATE_ADD function.

```sql
  SELECT tw.name, DATE_FORMAT(tw.whn,'%Y-%m-%d'), 
  tw.confirmed-lw.confirmed
  FROM covid tw LEFT JOIN covid lw ON 
    DATE_ADD(lw.whn, INTERVAL 1 WEEK) = tw.whn
    AND tw.name=lw.name
  WHERE tw.name = 'Italy'
  AND WEEKDAY(tw.whn)=0
  ORDER BY tw.whn;
```
---
6. This query shows the number of confirmed cases together with the world ranking for cases for the date '2020-04-20'. The number of COVID deaths is also shown.\
United States has the highest number, Spain is number 2...\
Notice that while Spain has the second highest confirmed cases, Italy has the second highest number of deaths due to the virus.\
**Add a column to show the ranking for the number of deaths due to COVID.**

```sql
  SELECT 
   name,
   confirmed,
   RANK() OVER (ORDER BY confirmed DESC) rc,
   deaths,
   RANK() OVER (ORDER BY deaths DESC) rd
  FROM covid
  WHERE whn = '2020-04-20'
  ORDER BY confirmed DESC;
```
---
7. This query includes a JOIN t the world table so we can access the total population of each country and calculate infection rates (in cases per 100,000).\
**Show the infection rate ranking for each country. Only include countries with a population of at least 10 million.**

```sql
  SELECT DISTINCT
   world.name,
   ROUND(100000*confirmed/population,2) infections,
   RANK() OVER (ORDER BY confirmed/population) rnk
  FROM covid JOIN world ON covid.name=world.name
WHERE whn = '2020-04-20' AND population > 10000000
ORDER BY population DESC;
```
