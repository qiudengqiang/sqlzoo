## SUM and COUNT

1. Show the total **population** of the world.

```mysql
SELECT SUM(population)
FROM world;
```

2. List all the continents - just once each.

```mysql
select distinct(continent)
from world;
```

3. Give the total GDP of Africa

```mysql
select sum(gdp)
from world
where continent='Africa';
```

4. How many countries have an **area** of at least 1000000

```mysql
select count(continent)
from world
where area>1000000;
```

5. What is the total **population** of ('Estonia', 'Latvia', 'Lithuania')

```mysql
select sum(population)
from world
where name in ('Estonia', 'Latvia', 'Lithuania');
```

6. For each **continent** show the **continent** and number of countries.

```mysql
select continent, count(name)
from world 
group by continent;
```

7. For each **continent** show the **continent** and number of countries with populations of at least 10 million.

```mysql
select continent,count(name)
from world
where population>10000000
group by continent;
```

8. List the continents that **have** a total population of at least 100 million.

```mysql
select continent
from world
group by continent having sum(population) > 100000000;
```

