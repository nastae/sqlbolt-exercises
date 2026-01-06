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