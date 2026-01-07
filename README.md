# SQLBolt exercises
Reference from [here](https://sqlbolt.com/lesson/).

# SQL Lesson 1: SELECT queries 101
1. Find the title of each film
```
SELECT title FROM movies;
```
2. Find the director of each film
```
SELECT director FROM movies;
```
3. Find the title and director of each film
```
SELECT title, director FROM movies;
```
4. Find the title and year of each film
```
SELECT title, year FROM movies;
```
5. Find all the information about each film
```
SELECT * FROM movies;
```
or
```
SELECT id, title, director, year, length_minutes FROM movies;
```

# SQL Lesson 2: Queries with constraints (Pt. 1) 
1. Find the movie with a row id of 6 
```
SELECT * FROM movies
WHERE id = 6;
```
2. Find the movies released in the years between 2000 and 2010 
```
SELECT * FROM movies
WHERE year BETWEEN 2000 AND 2010;
```
3. Find the movies not released in the years between 2000 and 2010
```
SELECT * FROM movies
WHERE year NOT BETWEEN 2000 AND 2010;
```
4. Find the first 5 Pixar movies and their release year ✓
```
SELECT * FROM movies
WHERE id <= 5;
```

# SQL Lesson 3: Queries with constraints (Pt. 2) 
1. Find all the Toy Story movies ✓
```
SELECT * FROM movies
WHERE title LIKE "Toy Story%";
```
2. Find all the movies directed by John Lasseter
```
SELECT * FROM movies
WHERE director = "John Lasseter";
```
3. Find all the movies (and director) not directed by John Lasseter
```
SELECT * FROM movies
WHERE director <> "John Lasseter";
```
or
```
SELECT * FROM movies
WHERE director != "John Lasseter";
```
4. Find all the WALL-* movie
```
SELECT * FROM movies
WHERE title LIKE "Wall-%";
```

# SQL Lesson 4: Filtering and sorting Query results 
1. List all directors of Pixar movies (alphabetically), without duplicates
```
SELECT DISTINCT director FROM movies
ORDER BY director;
```
2. List the last four Pixar movies released (ordered from most recent to least)
```
SELECT * FROM movies
ORDER BY year DESC
LIMIT 4;
```
3. List the first five Pixar movies sorted alphabetically
```
SELECT * FROM movies
ORDER BY title
LIMIT 5;
```
4. List the next five Pixar movies sorted alphabetically
```
SELECT * FROM movies
ORDER BY title
LIMIT 5 OFFSET 5;
```

# SQL Review: Simple SELECT Queries 
1. List all the Canadian cities and their populations ✓
```
SELECT * FROM north_american_cities
WHERE country = "Canada";
```
or
```
SELECT city, population FROM north_american_cities
WHERE country = "Canada";
```
2. Order all the cities in the United States by their latitude from north to south 
```
SELECT * FROM north_american_cities
WHERE country = "United States"
ORDER BY latitude DESC;
``` 
or
```
SELECT city FROM north_american_cities
WHERE country = "United States"
ORDER BY latitude DESC;
```
3. List all the cities west of Chicago, ordered from west to east
```
SELECT * FROM north_american_cities
WHERE longitude < "-87.629798"
ORDER BY longitude;
``` 
or
```
SELECT city FROM north_american_cities
WHERE longitude < "-87.629798"
ORDER BY longitude;
```
4. List the two largest cities in Mexico (by population) ✓
```
SELECT * FROM north_american_cities
WHERE country = "Mexico"
ORDER BY population DESC
LIMIT 2;
``` 
or
```
SELECT city FROM north_american_cities
WHERE country = "Mexico"
ORDER BY population DESC
LIMIT 2;
```
5. List the third and fourth largest cities (by population) in the United States and their population
```
SELECT * FROM north_american_cities
WHERE country = "United States"
ORDER BY population DESC
LIMIT 2 OFFSET 2;
``` 
or 
```
SELECT city FROM north_american_cities
WHERE country = "United States"
ORDER BY population DESC
LIMIT 2 OFFSET 2;
```

# SQL Lesson 6: Multi-table queries with JOINs 
1. Find the domestic and international sales for each movie
```
SELECT * FROM movies
INNER JOIN boxoffice ON movies.id = boxoffice.movie_id;
```
2. Show the sales numbers for each movie that did better internationally rather than domestically
```
SELECT * FROM movies
INNER JOIN boxoffice ON movies.id = boxoffice.movie_id
WHERE international_sales > domestic_sales;
``` 
or 
```
SELECT title, domestic_sales, international_sales FROM movies
INNER JOIN boxoffice ON movies.id = boxoffice.movie_id
WHERE international_sales > domestic_sales;
``` 
3. List all the movies by their ratings in descending order
```
SELECT * FROM movies
INNER JOIN boxoffice ON movies.id = boxoffice.movie_id
ORDER BY rating DESC;
``` 
or 
```
SELECT title FROM movies
INNER JOIN boxoffice ON movies.id = boxoffice.movie_id
ORDER BY rating DESC;
``` 

# SQL Lesson 7: OUTER JOINs
1. Find the list of all buildings that have employees ✓ 
```
SELECT DISTINCT building_name FROM employees
LEFT JOIN buildings ON employees.building = buildings.building_name;
```
2. Find the list of all buildings and their capacity
```
SELECT * FROM buildings;
```
or
```
SELECT building_name, capacity FROM buildings;
```
3. List all buildings and the distinct employee roles in each building (including empty buildings) 
```
SELECT DISTINCT building_name, role 
FROM buildings
LEFT JOIN employees ON buildings.building_name = employees.building;
```

# SQL Lesson 8: A short note on NULLs 
1. Find the name and role of all employees who have not been assigned to a building
```
SELECT * FROM employees
WHERE building IS NULL;
```
or
```
SELECT name, role FROM employees
WHERE building IS NULL;
```
2. Find the names of the buildings that hold no employees 
```
SELECT DISTINCT building_name FROM buildings
LEFT JOIN employees ON buildings.building_name = employees.building
WHERE employees.building IS NULL;
``` 

# SQL Lesson 9: Queries with expressions
1. List all movies and their combined sales in millions of dollars ✓
```
SELECT *, (domestic_sales + international_sales) / 1000000
FROM movies AS m
INNER JOIN boxoffice AS b ON m.id = b.movie_id;
```
or
```
SELECT title, (domestic_sales + international_sales) / 1000000
FROM movies AS m
INNER JOIN boxoffice AS b ON m.id = b.movie_id;
```
or
```
SELECT title, (domestic_sales + international_sales) / 1000000 AS sales
FROM movies AS m
INNER JOIN boxoffice AS b ON m.id = b.movie_id;
```
2. List all movies and their ratings in percent
```
SELECT title, rating * 10
FROM movies AS m
INNER JOIN boxoffice AS b ON m.id = b.movie_id;
``` 
or
```
SELECT title, rating * 10 AS rating_in_percent
FROM movies AS m
INNER JOIN boxoffice AS b ON m.id = b.movie_id;
```
3. List all movies that were released on even number years 
```
SELECT *
FROM movies AS m
WHERE m.year % 2 = 0;
``` 
or
```
SELECT title
FROM movies
WHERE year % 2 = 0;
```

# SQL Lesson 10: Queries with aggregates (Pt. 1)
1. Find the longest time that an employee has been at the studio 
```
SELECT MAX(years_employed) FROM employees;
``` 
or
```
SELECT MAX(years_employed) AS longest_time FROM employees;
```
2. For each role, find the average number of years employed by employees in that role 
```
SELECT *, AVG(years_employed) 
FROM employees
GROUP BY role;
``` 
or
```
SELECT *, AVG(years_employed) AS average_number_of_years_employed 
FROM employees
GROUP BY role;
```
or
```
SELECT role, AVG(years_employed) AS average_number_of_years_employed 
FROM employees
GROUP BY role;
```
3. Find the total number of employee years worked in each building ✓
```
SELECT building, SUM(years_employed) AS total_number_of_employee_years 
FROM employees
GROUP BY building;
```

# SQL Lesson 11: Queries with aggregates (Pt. 2) 
1. Find the number of Artists in the studio (without a HAVING clause) 
```
SELECT COUNT(*) FROM employees
WHERE role = "Artist";
``` 
or
```
SELECT COUNT(*) AS number_of_artists FROM employees
WHERE role = "Artist";
```
2. Find the number of Employees of each role in the studio 
```
SELECT COUNT(*), role FROM employees
GROUP BY role;
```
or
```
SELECT COUNT(*) AS number_of_employees, role FROM employees
GROUP BY role;
```
3. Find the total number of years employed by all Engineers 
```
SELECT SUM(years_employed) FROM employees
WHERE role = "Engineer";
``` 
or
```
SELECT SUM(years_employed) AS total_number_of_years_employed FROM employees
WHERE role = "Engineer";
```

# SQL Lesson 12: Order of execution of a Query 
1. Find the number of movies each director has directed 
```
SELECT director, COUNT(*) FROM movies
GROUP BY director;
``` 
2. Find the total domestic and international sales that can be attributed to each director
 
Wrong: 
```
SELECT director, SUM(domestic_sales) AS total_domestic_sales, SUM(international_sales) AS total_international_sales
FROM movies AS m
INNER JOIN boxoffice AS bo
ON m.id = bo.movie_id
GROUP BY director;
``` 
After searching, the correct query is:
```
SELECT director, SUM(domestic_sales + international_sales) AS total_sales
FROM movies AS m
INNER JOIN boxoffice AS bo
ON m.id = bo.movie_id
GROUP BY director;
```

# SQL Lesson 13: Inserting rows
1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)
```
INSERT INTO movies (title, director, year, length_minutes)
VALUES ("Toy Story 4", "John Lasseter", 2019, 100);
SELECT * FROM movies;   
```
2. Toy Story 4 has been released to critical acclaim! It had a rating of 8.7, and made 340 million domestically and 270 million internationally. Add the record to the BoxOffice table. 
```
INSERT INTO boxoffice (movie_id, rating, domestic_sales, international_sales)
VALUES (15, 8.7, 340000000, 270000000);
SELECT * FROM movies AS m
INNER JOIN boxoffice AS b
ON m.id = b.movie_id;
```

# SQL Lesson 14: Updating rows
1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter
 
Firstly, list movies with WHERE id = 2:
```
SELECT * FROM movies
WHERE id = 2;

UPDATE movies
SET director = "John Lasseter"
WHERE id = 2;
SELECT * FROM movies;
``` 
2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999
```
SELECT * FROM movies
WHERE id = 3;

UPDATE movies
SET year = 1999
WHERE id = 3;
SELECT * FROM movies;
``` 
3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich
```
SELECT * FROM movies
WHERE id = 11;

UPDATE movies
SET title = "Toy Story 3",
director = "Lee Unkrich"
WHERE id = 11;
SELECT * FROM movies;
```

# SQL Lesson 15: Deleting rows 
1. This database is getting too big, lets remove all movies that were released before 2005. 
```
SELECT * FROM movies
WHERE year < 2005;

DELETE FROM movies
WHERE year < 2005;
SELECT * FROM movies;
``` 
2. Andrew Stanton has also left the studio, so please remove all movies directed by him. 
```
SELECT * FROM movies
WHERE director = "Andrew Stanton";

DELETE FROM movies
WHERE director = "Andrew Stanton";
SELECT * FROM movies;
``` 

# SQL Lesson 16: Creating tables
1. Create a new table named Database with the following columns:
– Name A string (text) describing the name of the database
– Version A number (floating point) of the latest version of this database
– Download_count An integer count of the number of times this database was downloaded
This table has no constraints.
```
CREATE TABLE Database (
    Name TEXT,
    Version FLOAT,
    Download_count INTEGER
);
SELECT * FROM database;
``` 
