# SQLBolt training

SQL exercises from [sqlbolt.com](https://sqlbolt.com).

## SQL Lesson 1: SELECT queries 101

1. Find the title of each film
```sql
SELECT Title FROM movies;
```
2. Find the director of each film
```sql
SELECT Director FROM movies;
```
3. Find the title and director of each film
```sql
SELECT Title, Director FROM movies;
```
4. Find the title and year of each film
```sql
SELECT Title, Year FROM movies;
```
5. Find all the information about each film
```sql
SELECT * FROM movies;
```


## SQL Lesson 2: Queries with constraints (Pt. 1)

1. Find the movie with a row id of 6
```sqlSELECT * FROM movies
WHERE id = 6;
```
2. Find the movies released in the years between 2000 and 2010
```sql
SELECT * FROM movies
WHERE Year BETWEEN 2000 AND 2010;
```
3. Find the movies not released in the years between 2000 and 2010
```sql
SELECT * FROM movies
WHERE Year NOT BETWEEN 2000 AND 2010;
```
4. Find the first 5 Pixar movies and their release year
```sql
SELECT Title, Year FROM movies
LIMIT 5;
```


## SQL Lesson 3: Queries with constraints (Pt. 2)

1. Find all the Toy Story movies
```sql
SELECT * FROM movies
WHERE Title LIKE '%Toy Story%';
```
2. Find all the movies directed by John Lasseter
```sql
SELECT * FROM movies
WHERE Director = 'John Lasseter';
```
3. Find all the movies (and director) not directed by John Lasseter
```sql
SELECT Title, Director FROM movies
WHERE Director != 'John Lasseter';
```
4. Find all the WALL-* movies
```sql
SELECT Title FROM movies
WHERE Title LIKE 'WALL-_';
```


## SQL Lesson 4: Filtering and sorting Query results


1. List all directors of Pixar movies (alphabetically), without duplicates
```sql
SELECT DISTINCT Director FROM movies
ORDER BY Director;
```
2. List the last four Pixar movies released (ordered from most recent to least)
```sql
SELECT Title FROM movies
ORDER BY Year DESC
LIMIT 4;
```
3. List the first five Pixar movies sorted alphabetically
```sql
SELECT * FROM movies
ORDER BY Title ASC
LIMIT 5;
```
4. List the next five Pixar movies sorted alphabetically
```sql
SELECT title FROM movies
ORDER BY title ASC
LIMIT 5 OFFSET 5;
```


## SQL Review: Simple SELECT Queries


1. List all the Canadian cities and their populations
```sql
SELECT City, Population FROM north_american_cities
WHERE Country = 'Canada';
```
2. Order all the cities in the United States by their latitude from north to south
```sql
SELECT City, Country, Latitude FROM north_american_cities
WHERE Country = 'United States'
ORDER BY Latitude DESC;
```
3. List all the cities west of Chicago, ordered from west to east
```sql
SELECT City, Country, Longitude FROM north_american_cities
WHERE Longitude < -87.629798
ORDER BY Longitude ;
```
4.List the two largest cities in Mexico (by population)
```sql
SELECT City, Country, Population FROM north_american_cities
WHERE Country= 'Mexico'
ORDER BY Population DESC
LIMIT 2;
```
5. List the third and fourth largest cities (by population) in the United States and their population
```sql
SELECT City, Country, Population FROM north_american_cities
WHERE Country = 'United States'
ORDER BY Population 
LIMIT 2 OFFSET 2;
```


## SQL Lesson 6: Multi-table queries with JOINs

1. Find the domestic and international sales for each movie
```sql
SELECT Title, Domestic_sales, International_sales FROM Movies
INNER JOIN Boxoffice
ON id = Movie_id;
```
2. Show the sales numbers for each movie that did better internationally rather than domestically
```sql
SELECT Title, Domestic_sales, International_sales FROM Movies
INNER JOIN Boxoffice
ON id = Movie_id
WHERE International_sales > Domestic_sales;
```
3. List all the movies by their ratings in descending order
```sql
SELECT Title, Domestic_sales, International_sales FROM Movies
INNER JOIN Boxoffice
ON id = Movie_id
ORDER BY Rating DESC;
```
## SQL Lesson 7: OUTER JOINs

1. Find the list of all buildings that have employees
```sql
SELECT DISTINCT Building, Capacity FROM employees
INNER JOIN Buildings ON Building = Building_name;
```

2. Find the list of all buildings and their capacity

3. List all buildings and the distinct employee roles in each building (including empty buildings)
