## SELECT within SELECT Tutorial

1. List each country **name** **where the** **population** is larger than that of 'Russia'.

```mysql
select name 
from world
where population > (select population from world where name='Russia');
```

2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

```mysql
select name
from world
where gdp/population > 
(select gdp/population from world where name='United Kingdom') and continent='Europe';
```

3. List the **name** **and** **continent** **of countries in the continents containing either** **Argentina** **or** **Australia**. Order by name of the country.

```mysql
select name,continent
from world
where continent in (select continent from world where name in ('Argentina', 'Australia'))
ORDER BY name;
```

4. **Which country has a population that is more than Canada but less than Poland? Show the name and the population.**

```mysql
select name,population
from world
where population > (select population from world where name='Canada') 
and population < (select population from world where name='Poland');
```

5. **Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.**

```mysql
SELECT name, concat(round(100*population/(SELECT population FROM world WHERE name = 'Germany'),0), '%')
FROM world
WHERE continent = 'Europe'
```

6. **Which countries have a GDP greater than every country in Europe? [Give the** **name** **only.] (Some countries may have NULL gdp values)**

```mysql
select name
from world
where gdp>all(select gdp from world where gdp >=0 and continent='Europe')
and continent <> 'Europe';
```

7. **Find the largest country (by area) in each continent, show the** **continent****, the** **name** **and the** **area**

```mysql
select continent, name, area 
from world x
where area >= all(select area from world y where y.continent=x.continent and area>0);
```

8. **List each continent and the name of the country that comes first alphabetically.**

```mysql
select continent,name
from world x
where name<=all(select name from world y where x.continent=y.continent);
```

9. **Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show** **name****,** **continent** **and** **population**.

```mysql
select name,continent,population
from world x
where 25000000>all(select population from world y where x.continent=y.continent and population>0);
```

10. **Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.**

```mysql
select name,continent
from world x
where population > all(select 3*population from world y where x.continent=y.continent and population>0 and x.name<>y.name);
```

