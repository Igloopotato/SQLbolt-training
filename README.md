![sqlbolt](https://github.com/marswanttobeanalyst/SQLbolt-training/assets/141108687/b6881564-d040-41cb-b1f7-1812a8fe8e02)
# SQLBolt training

Welcome to my Repo! I've tackled every SQL problem I've encountered in this website that taught me on how to do SQL properly. Check out my solutions and let's talk SQL!
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
INNER JOIN Buildings ON Employees.Building = Buildings.Building_name;
```

2. Find the list of all buildings and their capacity
```sql
SELECT * FROM Buildings;
```

3. List all buildings and the distinct employee roles in each building (including empty buildings)
```sql
SELECT DISTINCT Building_name, Role FROM Buildings
LEFT JOIN Employees ON Buildings.Building_name = Employees.Building;
```

## SQL Lesson 8: A short note on NULLs

1. Find the name and role of all employees who have not been assigned to a building
```sql
SELECT * FROM employees
WHERE Building IS NULL;
```

2. Find the names of the buildings that hold no employees
```sql
SELECT Building_name, Role FROM Buildings LEFT JOIN Employees
ON Employees.Building = Buildings.Building_name
WHERE Role IS NULL;
```

## SQL Lesson 9: Queries with expressions

1. List all movies and their combined sales in millions of dollars
```sql
SELECT Title, (Domestic_sales+International_sales) /1000000 AS Total_sales_in_million FROM Movies
LEFT JOIN Boxoffice ON Movies.id = Boxoffice.Movie_Id;
```

2. List all movies and their ratings in percent
```sql
SELECT Title, Rating*10 AS Rating_percentage FROM Movies
LEFT JOIN Boxoffice ON Movies.id = Boxoffice.Movie_Id;
```

3. List all movies that were released on even number years
```sql
SELECT * FROM Movies
LEFT JOIN Boxoffice ON Movies.id = Boxoffice.Movie_Id
WHERE Year % 2 = 0;
```
## SQL Lesson 10: Queries with aggregates (Pt. 1)

1. Find the longest time that an employee has been at the studio
```sql
SELECT MAX(Years_employed) AS Longest_employed FROM employees;
```

2. For each role, find the average number of years employed by employees in that role
```sql
SELECT Role, AVG(Years_employed) AS AVG_employed FROM employees
GROUP BY Role;
```

3. Find the total number of employee years worked in each building
```sql
SELECT Building, SUM(Years_employed) AS Total_years_employed 
FROM employees
GROUP BY Building;
```
## SQL Lesson 11: Queries with aggregates (Pt. 2)

1. Find the number of Artists in the studio (without a HAVING clause)
```sql
SELECT Role, COUNT(ROLE) AS Number_artist FROM employees
WHERE Role = 'Artist'
GROUP BY Role;
```

2. Find the number of Employees of each role in the studio
```sql
SELECT Role, COUNT(ROLE) AS Number_artist FROM employees
GROUP BY Role;
```

3. Find the total number of years employed by all Engineers
```sql
SELECT Role, SUM(Years_employed) AS Total_years_employed FROM Employees
GROUP BY Role
HAVING Role = "Engineer";
```
## SQL Lesson 12: Order of execution of a Query

1. Find the number of movies each director has directed
```sql
SELECT Director, COUNT(Title) AS Number_Movie FROM Movies
JOIN Boxoffice ON Movies.Id = Boxoffice.Movie_Id
GROUP BY Director;
```

2. Find the total domestic and international sales that can be attributed to each director
```sql
SELECT Director, SUM(Domestic_sales) AS Total_Domestic_sales,
SUM(International_sales) AS Total_International_sales,
SUM(Domestic_sales+International_sales) AS Total_sales FROM Movies
JOIN Boxoffice ON Movies.id = Boxoffice.Movie_id
GROUP BY Director;
```
## SQL Lesson 13: Inserting rows

1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
```sql
INSERT INTO Movies
VALUES (4,'Toy Story 4', 'John Lasseter', 2023, 95);
```
2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table.
```sql
INSERT INTO Boxoffice
(Movie_id, Rating, Domestic_sales, International_sales)
VALUES (4, 8.7, 340000000, 270000000);
```

## SQL Lesson 14: Updating rows

1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
```sql
UPDATE movies
SET Director = 'John Lasseter'
WHERE Id = 2;
```

2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
```sql
UPDATE Movies
SET Year = 1999
WHERE Id = 3;
```

3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich
```sql
UPDATE Movies
SET Title = "Toy Story 3", Director = "Lee Unkrich"
WHERE Id = 11;
```

## SQL Lesson 15: Deleting rows

1.This database is getting too big, lets remove all movies that were released before 2005.
```sql
DELETE FROM Movies
WHERE Year < 2005;
```

2. Andrew Stanton has also left the studio, so please remove all movies directed by him.
```sql
DELETE FROM Movies
WHERE Director = 'Andrew Stanton';
```

## SQL Lesson 16: Creating tables

Create a new table named Database with the following columns:
– Name A string (text) describing the name of the database
– Version A number (floating point) of the latest version of this database
– Download_count An integer count of the number of times this database was downloaded
This table has no constraints.
```sql
CREATE TABLE Database (
    Name TEXT,
    Version FLOAT,
    Download_count INTEGER
);
```

## SQL Lesson 17: Altering tables

1.Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.
```sql
ALTER TABLE Movies
ADD Aspect_ratio FLOAT;
```

2.Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.
```sql
ALTER TABLE Movies
  ADD Language TEXT 
  DEFAULT "English";
```

## Lesson 18: Dropping tables

1.We've sadly reached the end of our lessons, lets clean up by removing the Movies table
```sql
DROP TABLE IF EXISTS Movies;
```

2. And drop the BoxOffice table as well
```sql
DROP TABLE BoxOffice;
```

 **THE END**
